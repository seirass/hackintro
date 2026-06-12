# Security Fundamentals — Lecture 1

## Security Mechanism Classification

Security mechanisms can be classified according to the property they provide:

### 1. Prevention
Prevent security incidents from occurring through precautionary measures.

### 2. Detection
Assuming an incident has occurred, detect it as early and accurately as possible.

### 3. Resilience
Assuming one or more incidents have occurred, ensure the system degrades gracefully rather than collapsing.

### 4. Deterrence
Discourage malicious behavior by ensuring penalties or consequences for responsible actors.

---

# Threat Modeling

Threat modeling is the process of identifying and enumerating potential threats, structural vulnerabilities, and missing safeguards, then prioritizing appropriate countermeasures.

## Components of a Threat Model

### 1. Assets
- What are you protecting?
- Which assets matter most?

### 2. System Goals

### 3. Adversary Definition & Risk Assessment

### 4. Threat Modeling Methodologies
- Diagram-based analysis
- Attack trees
- Checklists
- STRIDE
- MITRE ATT&CK
- Tactics, Techniques, and Procedures (TTPs)

---

# Four Key Security Properties

## 1. Confidentiality
Protecting information from unauthorized disclosure.

## 2. Integrity
Preventing unauthorized modification of data.

## 3. Authenticity
Ensuring actions and data can be attributed to the correct entity.

## 4. Availability
Ensuring resources remain accessible when needed.

---

# Trusted Computing Base (TCB)

A component's **Trusted Computing Base (TCB)** consists of all other components that must operate securely for that component to remain secure.

## Corollaries

1. If the TCB is secure, the component has a chance of being secure.
2. If the TCB misbehaves, no security guarantees can be made.

> **Trusted ≠ Trustworthy**

## Ideal TCB Design

### Verifiable
A TCB should be as small as possible to make verification practical.

### Tamper-Proof
The TCB must resist unauthorized modification (e.g., operating system or SSH daemon binaries).

## Why Do We Care About the TCB?

- Securing every component in a system is difficult.
- The TCB separates components that must be trusted from those that do not.
- Security efforts can be focused on the trusted portion of the system.

### Caveat
Determining the exact TCB is often difficult.

---

## Example Question

### Which of the following is **NOT** in the TCB of a web browser on your laptop?

A. The laptop's OS  
B. JavaScript downloaded from websites  
C. The laptop's hardware  
D. The browser's cryptographic library

**Answer:** B

The browser cannot guarantee that downloaded JavaScript is safe because it is entirely controlled by the website being visited.

---

# Key Security Principles

## 1. KISS (Keep It Simple, Stupid)

### Rule of Thumb
Software typically contains **1–5 defects per 1,000 lines of code (KLoC)**.

Examples:

| System | Approximate Lines of Code |
|----------|-------------------------|
| Windows 10 | 50 million |
| Linux Kernel | 27 million |
| seL4 Microkernel | 89 thousand |

A smaller and simpler TCB is easier to understand, verify, and secure.

---

## 2. Fail-Safe Defaults

The default action should be **deny access unless permission is explicitly granted**.

### Example

```c
void give_data(struct user){
    if(!user->pass == pass && user->name == name){
        return NULL;
    }
    return data;
}
```

This implementation violates fail-safe design because incorrect logic could accidentally grant access.

### Guiding Principle
> Default to denying access. Grant access only after successful authorization checks.

---

## 3. No Security Through Obscurity

### Common Fallacy
A system becomes more secure if its design remains secret.

### Problems with This Assumption

- Someone must implement the design.
- Users interact with the system.
- Designs are often distributed to many customers.
- Finding flaws in your own design is difficult.

Security should rely on strong mechanisms, not secrecy.

---

## 4. Complete Mediation

Every access to every object should be checked by a reference monitor.

### Challenge
This is difficult to implement correctly.

### Example Problem
**TOCTTOU (Time-of-Check to Time-of-Use)** vulnerabilities.

---

## 5. Least Privilege

Users and processes should receive only the permissions necessary to perform their tasks—and nothing more.

---

## 6. Separation of Duty

Critical tasks should require multiple individuals or approvals to complete.

---

## 7. Defense in Depth

Because individual security controls can fail:

- Use multiple layers of defense.
- Plan for failures.
- Beware of risk compensation.

---

# Practice Question

Systems based on Access Control Lists (ACLs), such as UNIX systems, typically deny access if a subject is not listed on the ACL.

Which security principle does this illustrate?

A. Fail-safe defaults  
B. Complete mediation  
C. Separation of duty  
D. Defense in depth

**Answer: A — Fail-safe defaults**

The default behavior is to deny access. Access is granted only when explicit authorization exists.
