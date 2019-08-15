## DOB NOW: Build Milestones

DOB NOW: Build is a self-service online tool from the [NYC Department of Buildings](https://www1.nyc.gov/site/buildings/index.page) that allows Building Owners, Design Professionals, Licensees, and Filing Representatives to conduct business with the Department online. DOB NOW provides customers with the ability to submit filings for construction work, check the status of a filing or inspection, pull permits, make renewals, and have virtual interactions with Agency staff. 

The DOB NOW Milestone application is a public-facing web interface that enables map-based navigation of the filings in DOB NOW. This application provides 2 different experiences for the user to choose from:
* Individual Filings: A user can search by job number, applicant name, or building address, and receive real-time information on a filing’s status, scope, and location. Key milestones of the filing process are displayed including the initial filing, plan review, objections, resubmissions, approval, permitting, and sign off.
* Multiple Filings: If the user chooses an applicant with multiple filings, or chooses the Multiple Filings option from the start, then they will be provided with the second experience: A map display of the entire list of search results. The filtered results are  displayed as a list with expandable details as well as a map of the filing location. If the user clicks on the Statistics tab, they'll see a series of charts that breaks down the trends within the user's search criteria, such as work types, filings statuses, and other location-based data insights. Users can also explore the results of their query by drilling down on individual filings. Selecting an individual record brings the user to the same individual filing page as referenced in the first module. 


![Milestone Map Page](https://github.com/cnicklin/DOB_NOW_Milestone_App/blob/gh-pages/MapPage.PNG)

## Data Source

Data flows from the BI tool to GitHub public hold. This is a daily automated process. It creates results in 2 formats: JSON (for search) and CSV (for map imaging).

<img align="center" width="" height="" src="https://github.com/cnicklin/DOB_NOW_Milestone_App/blob/gh-pages/Flow.PNG" alt="Milestone App Flow Diagram">

## Data Definitions
Definitions for elements on the Profile Page are listed below, but can also be viewed by hovering over the field name on the webpage.

### Profile Page

| Field Name | Definition |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Job Number | The unique ID number assigned when the applicant submits the filing to the Department of Buildings. |
| BIN Number | The Building Identification Number assigned by the Department of City Planning. |
| Work Type | The type of work described in this filing. It could include plumbing, sprinkler, construction fence, or another type of work. |
| Job Type | This indicates the extent of the work being done. NB means a new building is being built. A1 means that extensive alterations will be done resulting in a change of building occupancy. A2 means that alterations will be done but will not result in a change of building occupancy. A3 indicates that minor alterations will be done. |
| Professional Certification | Yes indicates that the applicant is certifying that the work being performed complies with all applicable laws and codes. This job will then skip review by a plan examiner. |
| Filing Status | The current status of the filing. A definition for each of the values for Filing Status can be found on our [Status Glossary](https://github.com/cnicklin/DOB_NOW_Milestone_App/blob/gh-pages/Statuses.md). |
| Number of Resubmissions | During review, the Department of Buildings may return a filing to the applicant multiple times because the information is incomplete, because it needs correction, or another reason. This indicates the total number of times the filing was resubmitted, and does not include the initial submission. |
| Job Description | The general description of the work being applied for. This field is free text, and is filled out by the applicant. |
| Total DOB Processing Time | The total number of business days that the filing has been under review by DOB from the inital submission to approval. |
| Total Time With Applicant | The total number of business days that the filing has been with the applicant for revision after inital submission and until approval. |

### Milestone Dates

| Field Name | Definition |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Initial Filing | The date that the applicant submitted the filing to the Department of Buildings. |
#| CPE Assigned | The date that the filing was assigned to a Chief Plan Examiner for review or for delegation to a Plan Examiner. |
| CPE Action | The date that the Chief Plan Examiner took action on the filing. |
| PE Assigned | The date that the filing was assigned to a Plan Examiner. |
| First Objection | The date that the filing was first returned to the applicant with objections. A filing may go through several cycles of being submitted, reviewed by a Plan Examiner, and returned to the applicant with objections. A filing may never receive objections and therefore may skip this milestone date. |
| Latest Objection | The most recent date that the filing was returned to the applicant with objections. A filing may never receive objections and therefore may skip this milestone date. |
| Latest Resubmission | The most recent date that the filing was resubmitted to the Department of Buildings for review. A filing may never be sent back to the applicant and therefore may skip this milestone date. |
| QA Supervisor Assigned | The date that the filing was assigned to a QA Supervisor for review or for delegation to a QA Admin. |
| QA Admin Assigned | The date that the filing was assigned to a QA Admin. |
| Initial QA Failed | The first date that the filing was returned to the applicant because it was incomplete or needed correction. A filing can fail QA multiple times, or it may be approved on the first review and skip this milestone date. |
| Plan Approved | The date that the filing was approved. The applicant can now pull permits. |
| Initial Permit Issued | The first date that a permit was issued. Multiple permits can be issued for a job filing. |
| Latest Permit Expiration | The expiration date for the most recent permit. Multiple permits can be issued for a job filing. |
| Job Signed Off | The date that the Department of Buildings acknowledged that the work is complete. |

### Milestone Timelines

To facilitate the design and layout of the Milestone Timeline in the Job Filing page, the following timelines were created. This reduces confusion that may be caused when a simpler timeline skips over a date, such as when a standard plan exam job never receives an objection.

Standard Plan Exam Timelines
<ol>
    <li>Standard Plan Exam with no objections: Initial Filing > CPE Assigned > CPE Action > PE Assigned > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Standard Plan Exam where the filing received its first objection (Filing Status = "Objections" and Resubmissions = 0): Initial Filing > CPE Assigned > CPE Action > PE Assigned > First Objection > Latest Objection > Latest Resubmission > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Standard Plan Exam where the filing received another objection (Filing Status = "Objections" and Resubmissions > 0): Initial Filing > CPE Assigned > CPE Action > PE Assigned > First Objection > Latest Resubmission > Latest Objection > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Standard Plan Exam with objections that has been resubmitted (Filing Status does not equal "Objections" and Resubmissions > 0): Initial Filing > CPE Assigned > CPE Action > PE Assigned > First Objection > Latest Objection > Latest Resubmission > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
</ol>

Professional Certification Timelines
<ol>
    <li>Pro-Cert with no QA failures: Initial Filing > QA Supervisor Assigned > QA Admin Assigned > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Pro-Cert with the first QA failure (Filing Status = "QA Failed" and Resubmissions = 0): Initial Filing > QA Supervisor Assigned > QA Admin Assigned > Initial QA Failed > Latest QA Failed > Latest Resubmission > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Pro-Cert where the filing failed QA another time (Filing Status = "QA Failed" and Resubmissions > 0): Initial Filing > QA Supervisor Assigned > QA Admin Assigned > Initial QA Failed > Latest Resubmission > Latest QA Failed > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
    <li>Pro-Cert with QA failures that has been resubmitted: Initial Filing > QA Supervisor Assigned > QA Admin Assigned > Initial QA Failed > Latest QA Failed > Latest Resubmission > Plan Approved > Initial Permit Issued > Latest Permit Expiration > Job Signed Off</li>
</ol>


## Built With

* [R](https://www.r-project.org/)
    + Core packages(dplyr, tidyr, RJDBC, ...)
* [Carto VL](https://carto.com/developers/carto-vl/)
* [Mapbox GL](https://www.mapbox.com/mapbox-gl-js/api/)
* [D3](https://d3js.org/)
* [Bootstrap](https://getbootstrap.com/)
* Java 1.6 (Core, open proj4j by osgeo)

## Built by

* [DOB Analytics and Data Science Team](https://www1.nyc.gov/site/buildings/about/metrics-reports.page) - If you have questions or feedback, comment here on github or email us at [Analytics@buildings.nyc.gov](mailto:analytics@buildings.nyc.gov). 

## Acknowledgments

* Inspired by [NYC Planning Labs](https://planninglabs.nyc/)

