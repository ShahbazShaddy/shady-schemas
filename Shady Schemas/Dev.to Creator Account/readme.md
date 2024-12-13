### **Web Data Source Integration Documentation**

#### **1. Data Source Overview**
- **Data Source Name:**  
  Dev.to Creator Verification  

- **Description:**  
  The Dev.to API endpoint allows for verifying if a user is marked as a creator on the Dev.to platform. This feature can help identify users who have been recognized as content creators.

---

#### **2. API Details**
- **API Endpoint URL:**  
  `https://dev.to/async_info/base_data`  

- **Request Method:**  
  `GET`  

- **Sample Response:**
  ```json
  {
      "broadcast": null,
      "param": "authenticity_token",
      "token": "some token",
      "user": "User info",
      "client_geolocation": "location",
      "default_email_optin_allowed": false,
      "creator": false
  }
  ```  

---

#### **3. Technical Breakdown**
- **Purpose in zkPass Framework:**  
  By using the `creator` field from the Dev.to API response, zkPass can generate a zk-proof that verifies whether a user is a recognized creator on the platform, without exposing additional personal details such as `user` or `client_geolocation`.  

- **Authentication Method:**  
  This endpoint may require prior user authentication on Dev.to. zkPass should securely manage user sessions or tokens if necessary.  

- **Validation Logic:**  
  - Extract the `creator` field from the API response.  
  - Verify that its value is `true` to confirm the user’s status as a creator.  

- **Security Considerations:**  
  - Avoid exposing sensitive fields such as `user` or `token`.  
  - Handle API responses securely, ensuring no sensitive data is stored beyond proof generation.  

---

#### **4. Schema Code**
Below is the JSON schema for integrating the Dev.to API with zkPass:

```json
{
  "issuer": "Dev.to",
  "desc": "This verifies if one is a valid creator on Dev.to.",
  "website": "https://dev.to/",
  "APIs": [
    {
      "host": "https://dev.to",
      "intercept": {
        "url": "async_info/base_data",
        "method": "GET"
      },
      "assert": [
        {
          "key": "creator",
          "value": "true",
          "operation": "="
        }
      ],
      "nullifier": "user"
    }
  ],
  "HRCondition": [
    "Must be a creator on Dev.to"
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```