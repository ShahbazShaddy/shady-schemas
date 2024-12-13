### **Overview: zkPass Integration Documentation**

---

#### **Introduction**
This document provides an overview of three integrations into the zkPass framework, each leveraging a unique API source for verification purposes. These integrations demonstrate how zkPass can create zk-proofs for various types of data while ensuring user privacy and data security.

---

#### **Integrated Data Sources**
1. **18+ Age verification**
   - **Description:**  
     Verifies if a user is over 18 years of age using Binance's KYC data.  
   - **API Endpoint:**  
     `https://www.binance.com/bapi/kyc/v1/private/kyc/user-kyc/get-personal-detail`  
   - **Key Feature:**  
     Uses the `birthday` field to check if the user's age is above 18.  
   - **Schema Highlights:**  
     - Nullifies the `personalName` for privacy.
     - Ensures compatibility with Binance's KYC verification systems.

2. **Dev.to Creator Verification**
   - **Description:**  
     Verifies if a user is a recognized content creator on Dev.to.  
   - **API Endpoint:**  
     `https://dev.to/async_info/base_data`  
   - **Key Feature:**  
     Utilizes the `creator` field to validate a user's creator status.  
   - **Schema Highlights:**  
     - Processes responses securely to avoid exposing sensitive data.
     - Designed for use cases like gating access to creator-exclusive features.

3. **Dev.to Follower Verification**
   - **Description:**  
     Confirms if a user is following a specific creator (CryptoAndy) on Dev.to.  
   - **API Endpoint:**  
     `https://dev.to/follows/bulk_show`  
   - **Key Feature:**  
     Checks the `2517749` field, which corresponds to CryptoAndy, to validate the follow status.  
   - **Schema Highlights:**  
     - Modular schema that can be adapted for other creators.
     - Minimal data extraction for enhanced privacy.

---

#### **Key Features of Integration**
- **Zero-Knowledge Proof Generation:**  
  zkPass ensures that only the necessary proof is generated without exposing sensitive user details like names, emails, or tokens.  

- **Dynamic API Handling:**  
  Each schema is designed to handle unique API requirements and validation logic, making it adaptable for future use cases.

- **Human-Readable Conditions (HRCondition):**  
  Simplified criteria are presented to users, e.g., "Must be over 18" or "Must follow CryptoAndy."

- **Tips for User Onboarding:**  
  Includes user-friendly messages guiding users through the verification process, ensuring seamless integration with zkPass workflows.

---

#### **Use Case Summary**
| **Integration**         | **Verification Purpose**                                                                                         | **Potential Use Case**                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| 18  Verification         | Confirms if a user is 18+ based on Binance KYC data.                                                            | Age-restricted services or products.                                     |
| Dev.to Creator Check     | Verifies if a user is a recognized content creator on Dev.to.                                                   | Access to creator-only programs, rewards, or communities.                |
| Dev.to Follower Check    | Confirms if a user follows a specific creator (CryptoAndy) on Dev.to.                                           | Gated access to content or exclusive groups for specific followers.      |

---

#### **Security Considerations**
- All integrations nullify sensitive user data (e.g., personalName, user info) after generating zk-proofs.
- APIs are securely intercepted, ensuring no sensitive data persists beyond proof validation.

---