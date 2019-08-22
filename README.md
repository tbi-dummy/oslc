
# Object Migration Package: #
Object Migration Package contains a list of customized OSLC's (as given below) and queries used by TBI to extract data from TRIRIGA.   
This package needs to be imported to the TRIRIGA intance to which TBI needs to integrate.   
Object migration Package is build with reference to the out-of-the-box Business Objects and forms provided by TRIRIGA.  

### Query/Reports:  ###
1. TBI triBuilding - Building details  
2. TBI triSpace - Space details   
3. TBI triSpaceLevelOccupancyAllocation - Organization Allocations details  

### OSLC Resource Manager:   ###
1. TBI triBuilding   
2. TBI triSpace    
3. TBI triOrganization 

### OSLC Manager:  ###
1. TBI triSpaceManagement   
   
## Import object migration package: ##

Import object migration package to any new TRIRIGA environment using the below steps:
1. Login to TRIRIGA UI
2. Upload the package to TRIRIGA:  
Home --> Object Migration(under 'Application Administration - Utilities') --> Click 'New Import Package' --> Click on 'Browse' in new pop-up --> Select Object migration zip file (TBI_TRIRIGA_PACKAGE.zip file in below link) and click 'OK'
  After package is uploaded, TRIRIGA will come back to 'Object Migration' page.
3. Validate and Import the package:  
Search for the 'TBI_TRIRIGA_Package' under 'Import packages' in 'Object Migraiton' page. Click on 'TBI_TRIRIGA_Package' to open the package --> Select 'Validate' and click on 'Wait' to wait for validation to complete ( Ensure that there are no conflicting in imports) --> Click on 'Import' and wait for couple of minutes for import to complete.   
On completion of import,  package will show as 'Imported' under 'status'.

## Object migration package: ##
https://github.com/tririga-building-insights/object-migration-package/releases/download/v1.0/TBI_TRIRIGA_Package.zip   

## Verification of Object migration package import: ##      
### OSLC API - Get Building details ###
1. Get call of building OSLC api with Basic authentication should provide 200 ok reponse code 
``` GET http://<tririgaIp:port>/tririga/oslc/spq/TBItriBuilding?oslc.select=* ```

2. Verify the existence of below fields with valid values in the response
	"spi:triCityTX"     
	"spi:triBuildingPathTX"      
	"spi:triBuildingHeadcountNU"    
	"spi:triCountryTX"   
	"spi:triGisLongitudeNU"    
	"spi:triGisLatitudeNU"    
	"spi:triBuildingIdTX"    
	"spi:triBuildingSYId"    
	"spi:triBuildingNameTX"   
	"spi:triStateProvTX"   
	"spi:triTimeZonesCL"   
	"spi:triModifiedSY"    

### OSLC API - Get Space details ###
1. Get call of space OSLC api with Basic authentication should provide 200 ok response code 
``` GET http://<tririgaIp:port>/tririga/oslc/spq/TBItriSpace?oslc.select=*,spi:TBItriOrganization{*}&oslc.where=spi:triBuildingPathTX="<BuildingPath>" ```

2. Verify the existence of below fields with valid values in the response  
	  "spi:triFloorLevelNU"  
    "spi:triSpaceNameTX"  
    "spi:triBuildingPathTX"  
    "spi:triSpaceAllocSeatsNU"  
    "spi:triFloordIdTX"  
    "spi:triFloorNameTX"  
    "spi:TBItriOrganization"  
    "spi:triBuildingSYId"  
    "spi:triSpaceHeadcountNU"  
    "spi:triFloorCapacityNU"  
    "spi:triFloorHeadcountNU"  
    "spi:triSpaceSYId"  
    "spi:triFloorSYId"  
    "spi:triSpaceCapacityNU"  
    "spi:triFloorPathTX"  
    
 A space which has a valid Occupancy Allocations , verify the existence of below fields with valid values under spi:TBItriOrganization in the response           
     "spi:triAllocHeadcountNU"     
     "spi:triNameTX"     
     "spi:triSYId"    
     "spi:triIdTX"    
     "spi:triPathTX"    
     "spi:triAllocSeatsNU"     
                    
## Space data - workstation and status considerations: ##
Space query filters the data for allocatable spaces and sends only the allocatable space details in the OSLC response. 
Allocatable space data is filtered using the below parameters.  
Workpoint=TRUE  
Assignable=TRUE  
Vacant Common!=TRUE  
Property Common!=TRUE  
Building Common!=TRUE  
Floor Common!=TRUE  

Spaces,Floors and Buildings with status as 'Retired','Deleted','Template' are excluded.


## Steps to remove the components imported through object migration package ##       
Below given are the steps to remove the components imported through object migration package in case if a customer want to remove the components imported through OSLC package if the TRIRIGA integration with TBI is no longer required. 

1. Login to TRIRIGA UI     
2. Delete the OSLC Resource Manager:    
a. Navigate to OSLC Resource Manager following the below path   
Home -> Tools -> System Setup -> Integration ->OSLC Resource Manager    
b. Search and select the OSLC Resource Managers with below Title and click 'Delete'   
 	TBI triBuilding   
 	TBI triSpace    
	TBI triOrganization     

3. Delete the OSLC Manager   
a. Navigate to OSLC Resource Manager following the below path  
Home -> Tools -> System Setup -> Integration ->OSLC Resource Manager    
b. Search and select the OSLC Manager with below Title and click 'Delete'   
TBI triSpaceManagement   

4. Delete the Query/Reports:     
a. Navigate to OSLC Resource Manager following the below path    
Home -> My Reports -> System Reports   
b. Search and select the reports with below Title and click 'Delete'   
TBI triBuilding - Building details  
TBI triSpace - Space details   
TBI triSpaceLevelOccupancyAllocation - Organization Allocations details   
  	
