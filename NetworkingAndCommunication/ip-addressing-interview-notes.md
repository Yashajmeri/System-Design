# IP Addressing – System Design Interview Notes

This document covers commonly asked **system design interview questions related to IP addressing**, with clear explanations, key points, and sample interview answers.

---

## 1. IPv4 vs IPv6

### What is the difference between IPv4 and IPv6?

Interviewers ask this to evaluate your understanding of **network scalability and addressing limitations**.

### Key Differences

#### Address Length
- **IPv4**: 32-bit address  
  Example: `192.168.1.1`
- **IPv6**: 128-bit address  
  Example: `2001:0db8:85a3::8a2e:0370:7334`

#### Address Format
- **IPv4**: Dotted decimal notation (`x.x.x.x`, where `0 ≤ x ≤ 255`)
- **IPv6**: Colon-separated hexadecimal notation

#### Scalability
- IPv4 has a **limited address space**
- IPv6 provides a **massive address pool** and supports auto-configuration

#### Security
- IPv6 has **built-in IPSec support**
- IPv4 requires additional configuration for encryption

### Sample Interview Answer
> IPv4 uses a 32-bit address space, which is limited and has led to address exhaustion. IPv6 uses a 128-bit address space, enabling massive scalability, better auto-configuration, and improved security with built-in IPSec support.

---

## 2. Why Do We Need Private IP Addresses?

### Purpose of Private IPs in System Design

Private IPs are used inside internal networks and are **not routable on the public internet**.

### Key Reasons

#### Address Conservation
- IPv4 addresses are limited
- Private IP ranges can be reused across organizations

#### Security
- Internal services are hidden from the public internet
- Reduces exposure to external attacks

#### Cost Efficiency
- Thousands of internal services can operate behind a **single public IP**

### Sample Interview Answer
> Private IPs allow organizations to design scalable internal networks while conserving public IP addresses. They improve security by isolating internal systems and reduce infrastructure costs.

---

## 3. How Does NAT Help Solve IPv4 Address Shortage?

### What is NAT?
**Network Address Translation (NAT)** maps private IPs to a public IP for outbound communication.

### Benefits of NAT

#### Address Reuse
- Multiple devices share a single public IP

#### Security
- Internal IP addresses are hidden from external networks

#### Scalability
- Enables ISPs and enterprises to support millions of users with limited public IPs

### Sample Interview Answer
> NAT helps mitigate IPv4 address exhaustion by allowing multiple devices to share a single public IP. It also adds a layer of security by hiding internal IP addresses.

---

## 4. How Do Load Balancers Distribute Traffic Using IPs?

Load balancers distribute incoming traffic across multiple servers to improve **availability and performance**.

### Load Balancing Techniques

#### 1. DNS Load Balancing
- A domain maps to multiple IP addresses
- DNS returns different IPs based on location or availability

#### 2. Layer 4 Load Balancing (Transport Layer)
- Routes traffic using **IP address and port**
- Faster but less flexible

#### 3. Layer 7 Load Balancing (Application Layer)
- Routes requests based on:
  - URLs
  - Headers
  - Cookies
  - Session data

### Sample Interview Answer
> Load balancers distribute traffic using DNS-based routing, transport-layer routing, or application-layer routing. This improves system reliability, scalability, and fault tolerance.

---

## 5. How Does DNS Resolve IP Addresses in Large-Scale Systems?

DNS resolution converts domain names into IP addresses through a hierarchical lookup process.

### DNS Resolution Flow

1. **Client Queries DNS Resolver**
   - Example: `example.com`

2. **Resolver Checks Cache**
   - Returns IP if cached, otherwise continues

3. **Root Server**
   - Directs request to the appropriate TLD server

4. **TLD Server**
   - Points to the authoritative DNS server

5. **Authoritative DNS Server**
   - Returns the final IP address

6. **Client Caches Result**
   - Improves future lookup performance

### Sample Interview Answer
> DNS resolution involves multiple hierarchical queries. Large-scale systems optimize this process using caching and CDNs to reduce latency and DNS load.

---

## Conclusion

- IPv4 and IPv6 are the core internet protocols, with IPv6 offering superior scalability
- Private IPs enable secure and cost-effective internal networking
- NAT extends the life of IPv4 by enabling IP sharing
- Load balancers distribute traffic efficiently using IP-based routing
- DNS is critical for resolving domain names in high-scale systems

---

## Interview Strategy & Key Takeaways

When answering system design questions:
1. **Define the concept**
2. **Explain why it matters**
3. **Give a real-world example** (e.g., AWS, Google, Netflix)

Mastering these fundamentals prepares you well for **SDE and backend system design interviews**.
