# SharePoint-UserProfile-Properties-using-JavaScript
SharePoint UserProfile Properties using JavaScript
```javascript
function getUserProperties()
{
//alert("Still working on it.") ;
var userID = NWF$('#' + varUserIdClientID).val();
var userFirstName = "";
var userLastName = ""; 
var userBU = "";
var userWorkPhone = "";
var webUrl = _spPageContextInfo.webAbsoluteUrl + "/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)?@v='" + "corp\\" + userID + "'"; 
console.log(webUrl);

NWF$.ajax  
    ({  
        url:webUrl,  
        type: 'GET',    
		async: false,  
        headers:    
		{ 
		"Accept": "application/json;odata=verbose"
		},  
		cache: false,  
	success: function(data)   
		{ 
		var results;
		
		if (data.d.UserProfileProperties == null || data.d.UserProfileProperties == "undefined")
		{
			userFirstName = "";
			userLastName = ""; 
			userBU = "";
			userWorkPhone = "";
		}	
		
		else if (data.d.UserProfileProperties.results.length > 0) 
		{ 
			results = data.d.UserProfileProperties.results;
			for (i = 0; i < results.length; i++)
			{
		
			if (results[i].Key == "FirstName") 
			{
			userFirstName = results[i].Value != null ? results[i].Value : "";
			}
	
			if (results[i].Key == "LastName") 
			{
			userLastName = results[i].Value != null ? results[i].Value : "";
			}
			
			if (results[i].Key == "Department") 
			{
			userBU = results[i].Value != null ? results[i].Value : "";
			}
			
			if (results[i].Key == "WorkPhone") 
			{
			userWorkPhone = results[i].Value != null ? results[i].Value : "";
			} 
	
			}
        }
		else
		{
			userFirstName = "";
			userLastName = ""; 
			userBU = "";
			userWorkPhone = "";
		}
	
		NWF$('#' + varUserFNameClientID).val(userFirstName);
		NWF$('#' + varUserLNameClientID).val(userLastName);
		NWF$('#' + varUserBUClientID).val(userBU);
		NWF$('#' + varUserWrkPhoneClientID).val(userWorkPhone);
	
   },
	error: function(xhr, status, error)  
   {  
		console.log("Error is " + error);    
		NWF$('#' + varUserFNameClientID).val("");
		NWF$('#' + varUserLNameClientID).val("");
		NWF$('#' + varUserBUClientID).val("");
		NWF$('#' + varUserWrkPhoneClientID).val("");	
   }   
}); 
}
```
