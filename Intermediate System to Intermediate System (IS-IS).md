# Intermediate System to Intermediate System (IS-IS)
***NET is the unique identifier for an IS-IS router, consisting of an Area ID, System ID, and NSEL.***
***Level 1 is for intra-area routing, while Level 2 is for inter-area routing.***
***Level 1-2 routers act as gateways between areas.***

### 1. Sending a Default Route to L1
### What Happens:

> The ABR advertises a default route (0.0.0.0/0) into the L1 area.
>
> This default route points to the ABR itself as the gateway to reach destinations outside the L1 area.
>
> Why It’s Used:
>
> implifies the L1 LSDB (Link-State Database) by reducing the number of routes.
>
> L1 routers only need to know about routes within their area and use the default route to reach external destinations.
>
### How It Works:
>
> L1 routers forward all traffic destined for external areas to the ABR.
>
> The ABR then routes the traffic through the L2 backbone.
>
> Key Characteristics:
>
> Less Routing Information: L1 routers do not have detailed information about L2 routes.
>
> Suboptimal Routing: Traffic may take a longer path because L1 routers do not know the best route to external destinations.
>
> Scalability: Reduces the size of the L1 LSDB, making it more scalable.
>
### 2. Route Leaking (Redistributing L2 Routes into L1)
### What Happens:
>
> The ABR selectively advertises specific L2 routes into the L1 area.
>
> This allows L1 routers to have detailed information about external destinations.
>
> Why It’s Used:
>
> Improves routing efficiency by allowing L1 routers to make better routing decisions.
>
> Avoids suboptimal routing by providing more specific route information.
>
> How It Works:
>
> The ABR leaks (redistributes) specific L2 routes into the L1 LSDB.
>
> L1 routers now have detailed information about external destinations and can choose the best path.
>
> Key Characteristics:
>
> More Routing Information: L1 routers have detailed knowledge of external routes.
>
> Optimal Routing: Traffic can take the most efficient path to external destinations.
>
> Increased LSDB Size: The L1 LSDB grows larger, which may impact scalability.
>
### Key Differences

| Feature        | Default Route to L1 | Route Leaking (L2 to L1) |
|---------------|--------------------|-------------------------|
| **Routing Information** | L1 routers only know about the default route. | L1 routers know specific external routes. |
| **Routing Efficiency** | Suboptimal routing (traffic may take longer paths). | Optimal routing (traffic takes the best path). |
| **LSDB Size** | Smaller LSDB in L1 area. | Larger LSDB in L1 area due to additional routes. |
| **Scalability** | More scalable for large networks. | Less scalable due to increased LSDB size. |
| **Configuration** | Simpler to configure. | Requires careful configuration to avoid excessive route leakage. |



### When to Use Each Approach
**Default Route to L1:**
>
> Use in large networks where scalability is a concern.
>
> Suitable when suboptimal routing is acceptable.
>
**Route Leaking:**

> Use when optimal routing is critical.
>
> Suitable for smaller networks or when specific external routes need to be advertised.

**Example Scenario**
**Default Route:**

> An ABR in Area 1 advertises a default route to L1 routers.
>
> L1 routers forward all external traffic to the ABR, which then routes it through the L2 backbone.

**Route Leaking:**

> The ABR leaks specific L2 routes (e.g., 10.1.0.0/16) into Area 1.
>
> L1 routers in Area 1 now know the exact path to 10.1.0.0/16 and can route traffic directly.

**Summary**
>
> **Default Route:** Simplifies routing and improves scalability but may lead to suboptimal paths.
>
> **Route Leaking:** Provides optimal routing but increases the size of the L1 LSDB and requires careful configuration.
