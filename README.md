# ⏱️ Time-Based IAM Policy Using AWS IAM

## 📌 Overview

This project demonstrates how to create and apply a **time-based IAM policy** in AWS.
A time-based policy allows access to AWS services **only within a defined time window** using IAM policy conditions. After the specified time expires, the policy remains attached but becomes **inactive automatically**.

---

## 🎯 Use Case

* Grant **temporary access** to AWS resources
* Enforce **time-bound security controls**
* Reduce risk by automatically expiring permissions
* Useful for:

  * Interns / trainees
  * Temporary contractors
  * Short-term access scenarios

---

## 🧩 AWS Services Used

* **AWS IAM**
* **Amazon S3**

---

## 🏗️ Architecture Summary

* An IAM policy is created with **date-based conditions**
* The policy allows **read and list** access to S3
* Access is restricted using `aws:CurrentTime`
* Policy is attached to a specific IAM user
* After the defined time expires → **Access Denied**

---

## 🔐 Policy Behavior

| Action                        | Result          |
| ----------------------------- | --------------- |
| List S3 buckets (within time) | ✅ Allowed       |
| Read objects (within time)    | ✅ Allowed       |
| Upload objects                | ❌ Denied        |
| Any action after expiry       | ❌ Access Denied |

---

## 🛠️ Implementation Steps (High Level)

1. Create an IAM policy using **Visual Editor**
2. Select **Amazon S3** as the service
3. Allow actions:

   * `ListBucket`
   * `GetObject`
4. Configure **Request Conditions**

   * Condition Key: `aws:CurrentTime`
   * Operator: Date-based condition
   * Time format: **UTC**
5. Review and create the policy
6. Attach the policy to an IAM user
7. Test access before and after time expiry

---

## 🧪 Validation & Testing

* ✅ IAM user can list and read S3 buckets **before time expiry**
* ❌ IAM user cannot upload objects (no write permission)
* ❌ IAM user gets **Access Denied** after time expires

---

## 🧠 Key Learnings

* IAM policies can be **time-restricted**
* Conditions enhance **security granularity**
* Policies remain attached but **stop working automatically**
* No manual revocation needed after expiry

---

## 📎 Sample Condition Used

```json
"Condition": {
  "DateLessThan": {
    "aws:CurrentTime": "2025-11-21T19:33:55Z"
  }
}
```

---

## 🚀 Future Enhancements

* Add **region-based restrictions**
* Combine with **IP-based conditions**
* Automate using **CloudFormation / Terraform**
* Add **CloudTrail** for auditing access

---

## 📄 Documentation Source

This README is created based on the implementation steps and screenshots provided in the uploaded document. 
 
