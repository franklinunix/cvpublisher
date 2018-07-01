# cvpublisher
Ansible role used to demonstrate automated Satellite monthly content view publication.

## Overview

This role is quite simple. It takes several variables needed to identify content views, their errata by date content filters, a new end date for the filter (typically set to the first of the month), and then updates the filters and publishes the content views. Ideally this becomes a project in your ansible tower instance and is scheduled to run after the first of the month. The end date and schedule date are arbitrary and can easily be controlled. 


## Detail

When building CVs in Satellite for managing environments through time it is typical to create several content filters on RPM packages. First we create a filter than includes all packages that have no errata published. Secondly we create a filter that includes all errata (sometimes of a given type, i.e. bugfix, security or enhancement errata) that have been published up until a given date. This allows us to produce system images that have a consistent, well-known content. Our goal is standardization, repeatability and automation.

The role uses the following variables:

organization - the Satellite organization under which the plays will find the specified content views.
base_soes - these our the BASE Standard Operating Environment content views on which our other content views are built. These content views will be published synchronously to ensure that when we publish the others, they will complete without timing out.
content_views - these are the remaining, non-composite content views that we will updated the errata on. These can be published asynchronously as they are typically smaller than our base soe and publish quickly.
composite_content_views - these are content views that require all the non-composite views to be published first. 
content_view_filter - this is the standardized name for the Errata By Date filter - e.g. IncludeErrataByDate
end_date - this is the new end date for the above include filter. 

This role can be extended to allow for more complex publishing. Automated discovery of base soes, non-composite and composite views, multiple filter types with different dates, etc.. 

The goal of this module was to demonstrate the possibility and make taking care of my lab easier :-)
