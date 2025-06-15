
# 🌐 Travel-Bank_Resilience4j_v8 🚀

> 🛡️ Advanced Resiliency Patterns with Spring Cloud Gateway and Resilience4j

This project enhances the **Travel Bank Microservices Suite** by integrating **Resilience4j** patterns into the **Spring Cloud Gateway**, building on top of the previous modules in the suite.

---

## 🔁 Key Resilience Patterns Implemented

### ⚡ Circuit Breaker
Stops invoking failing services to allow recovery.

### ♻ Retry
Retries transient failed requests with backoff support.

### 🚦 Rate Limiter
Controls number of requests in a time window (to avoid abuse).

### ⛔ Bulkhead
Limits concurrent requests to protect system from overload.

### 🧰 Fallback
Provides alternative paths when a service call fails.

---

## 🏗️ Architecture Flow

```
Client → Gateway (Resilience Filters: RateLimiter, CircuitBreaker, Bulkhead, Retry) → Eureka Discovery → Microservices
```

Each request flows through multiple filters ensuring resiliency before reaching the actual service.

---

## 📦 Project Module Lineage

| Version | 📁 Module                                   | 🔍 Description |
|---------|---------------------------------------------|----------------|
| [v1.0](https://github.com/vinaysteja2/TRAVEL-BANK_Micorservices_v_1.git) | Microservices Core | Base services: accounts, loans, cards |
| [v2.0](https://github.com/vinaysteja2/TRAVEL-BANK_Docker_v_2.git) | Dockerization | Containerization of services |
| [v3.0](https://github.com/vinaysteja2/Travel-Bank_Config_Management_v_3.git) | Config Management | Central config via Spring Cloud Config |
| [v4.0](https://github.com/vinaysteja2/Travel-Bank_ConfigServer_v_4.git) | Config Server | Hosting shared properties |
| [v5.0](https://github.com/vinaysteja2/Travel-Bank_MySqlDB_v_5.git) | MySQL DB | MySQL-based persistent storage |
| [v6.0](https://github.com/vinaysteja2/Travel-Bank_ServiceRegistry_v6) | Service Registry | Eureka-based discovery |
| [v7.0](https://github.com/vinaysteja2/Travel-Bank_Gateway_v7) | Gateway | Spring Cloud Gateway |
| ⭐ [v8.0] | Resilience | Resilience4j with Spring Gateway |

---

## 🔧 Configuration Highlights

```yaml
resilience4j:
  circuitbreaker:
    instances:
      accountsCircuitBreaker:
        slidingWindowSize: 10
        permittedNumberOfCallsInHalfOpenState: 2
        failureRateThreshold: 50
        waitDurationInOpenState: 10s

  retry:
    instances:
      retryService:
        maxAttempts: 3
        waitDuration: 2s

  ratelimiter:
    instances:
      rateLimitService:
        limitForPeriod: 10
        limitRefreshPeriod: 1s
        timeoutDuration: 0

  bulkhead:
    instances:
      bulkheadService:
        maxConcurrentCalls: 5
        maxWaitDuration: 1s
```

---

## 🧪 Running the Gateway

1. Start Eureka from v6.0  
2. Start microservices from v1.0  
3. Start Gateway from v7.0  
4. Run **Travel-Bank_Resilience4j_v8**

Access:
```
GET http://localhost:8080/accounts/api/v1/getDetails
```

---

## 📄 Real-World Usage Scenario

Imagine a client sending multiple requests to the `/accounts` API.

- If `/accounts` is down → fallback is triggered.
- If traffic spikes → rate limiter kicks in.
- If there's temporary failure → retry mechanism activates.
- If system is overloaded → bulkhead restricts access.

All this ensures better uptime, fair usage, and graceful degradation.

---

## 💬 Contribution

Fork this repository, create your feature branch and submit a PR. Contributions welcome!

---

## 📜 License

MIT License © [Vinay Steja](https://github.com/vinaysteja2)

Built with 💙 using Spring Boot, Spring Cloud Gateway & Resilience4j
