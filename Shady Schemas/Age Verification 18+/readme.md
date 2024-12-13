### **Web Data Source Integration Documentation**

#### **1. Data Source Overview**
- **Data Source Name:**  
  Binance KYC API  

- **Description:**  
  The Binance KYC API allows access to user personal details, enabling verification of specific information such as name and date of birth. This is particularly useful for age verification scenarios, ensuring compliance with regulations that require users to be over 18 years of age.

---

#### **2. API Details**
- **API Endpoint URL:**  
  `https://www.binance.com/bapi/kyc/v1/private/kyc/user-kyc/get-personal-detail`  

- **Request Method:**  
  `GET`  

- **Sample Response:**
  ```json
  {
      "code": "000000",
      "message": null,
      "messageDetail": null,
      "data": {
          "personalName": "My Name",
          "birthday": "2003-01-01"
      },
      "success": true
  }
  ```  

---

#### **3. Technical Breakdown**
- **Purpose in zkPass Framework:**  
  By using Binance KYC data, zkPass can generate a zk-proof that verifies whether a user is above 18 years of age without revealing the user's full personal details.  

- **Authentication Method:**  
  Authentication may require user login or API keys (not detailed in the sample, but essential for a private endpoint). zkPass should securely handle these credentials.

- **Validation Logic:**  
  - Extract the `birthday` field from the API response.  
  - Check if the date is earlier than January 1, 2006, to confirm if the user is over 18 years old.  

- **Security Considerations:**  
  - Ensure API response data is handled securely.  
  - Mask sensitive information such as `personalName` during zk-proof generation.  
  - Use HTTPS for secure API communication.

---

#### **4. Schema Code**
Below is the JSON schema for integrating Binance KYC with zkPass:

```json
{
  "issuer": "Binance",
  "desc": "The platform to ask questions and connect with people who contribute unique insights and quality answers.",
  "website": "https://www.binance.com/en/my/settings/kyc",
  "APIs": [
    {
      "host": "https://www.binance.com/",
      "intercept": {
        "url": "bapi/kyc/v1/private/kyc/user-kyc/get-personal-detail",
        "method": "GET"
      },
      "assert": [
        {
          "key": "data|birthday",
          "value": "2006-01-01",
          "operation": "<"
        }
      ],
      "nullifier": "data|personalName"
    }
  ],
  "HRCondition": [
    "Must Born Before 2006"
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
