# DNS – System Design Interview Notes

This document covers **commonly asked DNS interview questions** with structured explanations, performance considerations, and real-world relevance for large-scale systems.

---

## 1. DNS Resolution Process (Step-by-Step)

DNS (Domain Name System) resolves human-readable domain names into IP addresses.

### DNS Resolution Flow

1. **User Query**
   - User enters a domain name (e.g., `www.example.com`) in the browser.

2. **Browser Cache Check**
   - Browser checks if the IP is already cached.

3. **Operating System Cache Check**
   - If not found in the browser, the OS resolver checks its local cache.

4. **Recursive DNS Resolver Query**
   - If still unresolved, the request is sent to a recursive resolver (usually ISP or public DNS).

5. **Root DNS Server**
   - If the resolver has no cached result, it queries one of the root DNS servers.

6. **TLD Server**
   - The root server points to the Top-Level Domain (TLD) server (e.g., `.com`, `.org`).

7. **Authoritative DNS Server**
   - The TLD server provides the authoritative DNS server for the domain.

8. **IP Address Retrieval**
   - The authoritative server returns the correct IP address.

9. **Response Caching**
   - The resolver caches the response for future queries.

10. **Website Access**
    - Browser uses the IP address to connect to the web server.

### Interview Tip
> Emphasize **caching** and **hierarchical lookup** to show scalability awareness.

---

## 2. Recursive vs Authoritative DNS Servers

### Recursive DNS Server
- Acts as an intermediary for the client
- Performs the entire DNS lookup process
- Typically provided by:
  - ISPs
  - Google Public DNS
  - Cloudflare DNS

### Authoritative DNS Server
- Stores actual DNS records:
  - A, AAAA, CNAME, MX, etc.
- Provides the **final answer**
- Managed by:
  - Domain owners
  - Hosting providers

### Key Difference
> Recursive servers **fetch DNS data**, while authoritative servers **store and serve the source of truth**.

---

## 3. DNS Caching – Performance Optimization

DNS caching stores previously resolved DNS records to speed up future lookups.

### Benefits of DNS Caching
- Reduced latency
- Lower DNS server load
- Faster website access
- Improved user experience

### Where DNS Caching Occurs

| Layer | Description |
|-----|------------|
| Browser Cache | Stores DNS results for visited sites |
| OS Cache | Maintains system-level DNS cache |
| Recursive Resolver | Caches responses for multiple users |

### Interview Insight
> DNS caching is critical for **high-traffic applications** like Netflix and Google.

---

## 4. TTL (Time-To-Live) in DNS

### What is TTL?
TTL defines how long a DNS record is considered valid before it must be refreshed.

### Why TTL Matters

- **Short TTL** (e.g., 60s)
  - Faster updates
  - Higher DNS query load

- **Long TTL** (e.g., 24 hours)
  - Fewer queries
  - Slower propagation of changes

### Trade-off
> TTL balances **performance vs freshness** of DNS records.

---

## 5. DNS-Based Load Balancing in Large-Scale Systems

DNS can distribute traffic by returning different IPs for the same domain.

### DNS Load Balancing Techniques

#### Round-Robin DNS
- Cycles through multiple IP addresses
- Simple but no health checks

#### Geo-Based Routing
- Routes users to nearest data center
- Reduces latency

#### Failover DNS
- Removes unhealthy servers
- Improves availability

#### Anycast DNS
- Same IP advertised from multiple locations
- Routes to nearest server automatically

### System Design Use Case
> Used by CDNs, cloud providers, and global web platforms.

---

## 6. DNS Security Threats & Mitigations

### Common DNS Attacks

#### DNS Spoofing / Cache Poisoning
- Injects fake DNS records
- Redirects users to malicious sites
- **Mitigation**: DNSSEC

#### DDoS Attacks on DNS
- Overloads DNS infrastructure
- **Mitigation**:
  - Rate limiting
  - Anycast DNS
  - Load balancing

#### Man-in-the-Middle (MITM) Attacks
- Intercepts DNS queries
- **Mitigation**:
  - DNS-over-HTTPS (DoH)
  - DNS-over-TLS (DoT)

#### NXDOMAIN Attacks
- Floods resolvers with non-existent domain queries
- **Mitigation**:
  - Response Rate Limiting (RRL)
  - DNS firewalls

### Key Takeaway
> DNS security is essential for **availability, trust, and data integrity**.

---

## Final Interview Takeaways

- DNS is a **hierarchical, distributed system**
- Caching is key to scalability
- TTL impacts both performance and correctness
- DNS plays a major role in **load balancing and failover**
- Security mechanisms like DNSSEC and DoH are critical at scale

---

## Interview Answer Strategy

When answering DNS questions:
1. Explain the **flow**
2. Mention **caching & performance**
3. Add **real-world scale examples**
4. Discuss **failure and security scenarios**
