### **Web Data Source Integration Documentation**

---

#### **1. Data Source Overview**
- **Data Source Name:**  
  Dev.to Follower Verification for CryptoAndy  

- **Description:**  
  This integration verifies if a user follows CryptoAndy on Dev.to by checking the response from the `follows/bulk_show` API endpoint.

---

#### **2. API Details**
- **API Endpoint URL:**  
  `https://dev.to/follows/bulk_show`  

- **Request Method:**  
  `GET`  

- **Sample Response:**
  ```json
  {
      "2517749": "true"
  }
  ```
  - **Note:**  
    The key `2517749` represents CryptoAndy's unique user ID on Dev.to. If the value is `"true"`, it confirms that the user is following CryptoAndy.

---

#### **3. Technical Breakdown**
- **Purpose in zkPass Framework:**  
  This verification allows zkPass to generate a zk-proof that confirms a user follows CryptoAndy on Dev.to without revealing their personal details or other followings.

- **Authentication Method:**  
  The API may require user authentication. zkPass should ensure secure session handling and avoid storing sensitive tokens.  

- **Validation Logic:**  
  - Extract the field corresponding to the key `2517749`.  
  - Verify that its value is `"true"`.  

- **Security Considerations:**  
  - Ensure only the required key (`2517749`) is extracted and processed.  
  - Securely handle API responses to avoid unintended exposure of user follow data.  

---

#### **4. Schema Code**
Here is the JSON schema for the integration:

```json
{
  "issuer": "Dev.to",
  "desc": "This verifies if one is following CryptoAndy on Dev.to.",
  "website": "https://dev.to/cryptosandy",
  "APIs": [
    {
      "host": "https://dev.to/",
      "intercept": {
        "url": "follows/bulk_show",
        "method": "GET"
      },
      "assert": [
        {
          "key": "2517749",
          "value": "true",
          "operation": "="
        }
      ]
    }
  ],
  "HRCondition": [
    "Must follow CryptoAndy on Dev.to"
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```

---