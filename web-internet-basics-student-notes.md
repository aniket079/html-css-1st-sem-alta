# Web & Internet Engineering: Comprehensive Study Notes

---

## Module 1: Introduction to Web & Internet

### 1.1 The Internet vs. The World Wide Web

Although used interchangeably in everyday language, the **Internet** and the **World Wide Web (WWW)** are fundamentally different technologies operating at different levels of the networking stack.

```
+-----------------------------------------------------------------------+
|                    THE WORLD WIDE WEB (Application)                   |
|   (Websites, HTML Pages, HTTP/HTTPS, Web Browsers, REST APIs, Audio)  |
+-----------------------------------------------------------------------+
|                         THE INTERNET (Infrastructure)                 |
|   (Fiber Cables, Routers, IP Addresses, TCP/UDP, Packets, Hardware)   |
+-----------------------------------------------------------------------+
```

| Dimension | The Internet | The World Wide Web |
| :--- | :--- | :--- |
| **Definition** | A global network of interconnected computer networks (hardware infrastructure). | An information system of interlinked documents and resources accessed via the Internet. |
| **Nature** | Physical hardware, underground cables, satellites, routers, switches. | Software service, protocols, web pages, hypermedia, web servers. |
| **Core Protocol** | TCP/IP, IP, BGP | HTTP / HTTPS |
| **Identifiers** | IP Addresses (e.g., `192.168.1.1`) | URLs / URIs (e.g., `https://www.example.com`) |
| **Invention / Era** | ARPANET (Late 1960s) / TCP/IP standard (1983) | Tim Berners-Lee at CERN (1989) |

---

### 1.2 How Data Travels: Packet Switching

The Internet operates as a **packet-switched network**. Large data files (such as web pages, images, or videos) are not transmitted as a single continuous stream. Instead, they are broken down into small units called **packets**.

```
[ Sender Device ]
       │
       ├─► [ Packet 1 ] ──► (Router A) ──► (Router C) ┐
       ├─► [ Packet 2 ] ──► (Router B) ───────────────┼──► [ Receiver Device ]
       └─► [ Packet 3 ] ──► (Router A) ──► (Router D) ┘   (Reassembles Packets)
```

#### Key Characteristics of Packet Switching:
1. **Packet Structure**: Each packet contains:
   * **Header**: Contains metadata including Source IP, Destination IP, Packet Sequence Number, and Protocol Type.
   * **Payload**: The actual chunk of data being transmitted.
   * **Trailer**: Error-checking bits (Checksum) to detect corruption during transmission.
2. **Dynamic Routing**: Packets taking different paths across global routers based on network traffic and bandwidth.
3. **Reassembly**: The destination host receives packets out of order, uses sequence numbers to reorder them, and reassembles the original file.

---

### 1.3 Client-Server Architecture

Web communication relies primarily on the **Client-Server Architecture**, a distributed application structure that partitions tasks between service providers (servers) and service requesters (clients).

```
                      1. HTTP Request (e.g., GET /index.html)
        ┌──────────────────────────────────────────────────┐
        │                                                  │
┌───────┴────────┐                                 ┌───────▼────────┐
│   Web Client   │                                 │   Web Server   │
│  (Browser/App) │                                 │ (Apache/Nginx) │
│ IP: 198.51.100.2                                 │ IP: 93.184.216.34
└───────▲────────┘                                 └───────┬────────┘
        │                                                  │
        └──────────────────────────────────────────────────┘
                      2. HTTP Response (200 OK + HTML Body)
```

#### The Client:
* **Role**: Initiates communication by sending requests.
* **Examples**: Web browsers (Chrome, Firefox, Safari), mobile apps, CLI utilities (`curl`).
* **Responsibility**: Rendering user interfaces, handling user inputs, parsing HTML/CSS/JavaScript, and dispatching asynchronous HTTP requests.

#### The Server:
* **Role**: Listens continuously on network ports for incoming requests, processes requests, and returns responses.
* **Examples**: Nginx, Apache HTTP Server, Node.js, IIS.
* **Responsibility**: Hosting assets, database access, executing backend business logic, handling authentication, and serving HTTP content.

---

### 1.4 IP Addresses and Port Numbers

For two network devices to communicate, they require both an address to locate the machine (**IP Address**) and a specific channel to locate the application on that machine (**Port Number**).

```
        Network Address (Machine)      Application Channel
        ┌───────────────────────┐      ┌───┐
        │     93.184.216.34     │  :   │ 80│  (HTTP Web Service)
        └───────────────────────┘      └───┘
```

#### Standard System Port Numbers:
* **Port 80**: Default port for unencrypted Web Traffic (**HTTP**).
* **Port 443**: Default port for encrypted Web Traffic (**HTTPS**).
* **Port 22**: Secure Shell (**SSH**) remote login.
* **Port 53**: Domain Name System (**DNS**) resolution queries.
* **Port 21**: File Transfer Protocol (**FTP**).

---

## Module 2: Internet Protocols & Architecture

### 2.1 The TCP/IP Protocol Suite

Communication across the Internet is governed by the **TCP/IP Model**, an open-standard 4-layer networking framework.

```
+-----------------------------------------------------------------------+
|  4. APPLICATION LAYER   (HTTP, HTTPS, DNS, FTP, SSH, SMTP)             |
|     Creates the user data payload.                                    |
+-----------------------------------------------------------------------+
|  3. TRANSPORT LAYER     (TCP, UDP)                                    |
|     Manages end-to-end communication, ports, reliability.             |
+-----------------------------------------------------------------------+
|  2. INTERNET LAYER      (IP - IPv4/IPv6, ICMP)                        |
|     Packs data into packets, handles logical IP routing across nodes. |
+-----------------------------------------------------------------------+
|  1. LINK / PHYSICAL     (Ethernet, Wi-Fi 802.11, Fiber Optic)         |
|     Converts binary packets into physical electrical/optical signals. |
+-----------------------------------------------------------------------+
```

---

### 2.2 IPv4 vs. IPv6 Addressing

| Feature | IPv4 (Internet Protocol v4) | IPv6 (Internet Protocol v6) |
| :--- | :--- | :--- |
| **Address Length** | 32 bits (4 bytes) | 128 bits (16 bytes) |
| **Total Pool Size** | ~4.3 Billion ($2^{32}$) | ~$3.4 \times 10^{38}$ ($2^{128}$) |
| **Notation Format** | Dot-Decimal: `192.168.1.1` | Hexadecimal Colon: `2001:0db8:85a3::8a2e:0370:7334` |
| **Configuration** | Manual or via DHCP | Auto-configuration (SLAAC) or DHCPv6 |
| **Security** | Security features optional (IPsec added later) | IPsec support mandatory in original design |

---

### 2.3 Transport Layer Protocols: TCP vs. UDP

```
        TCP (Transmission Control Protocol)             UDP (User Datagram Protocol)
   Connection-Oriented, Reliable, Ordered         Connectionless, Fast, Unchecked

      Client              Server                     Client              Server
        │                   │                          │                   │
        ├─── SYN ──────────►│                          ├─── Datagram 1 ───►│
        │◄── SYN-ACK ───────┤                          ├─── Datagram 2 ───►│
        ├─── ACK ──────────►│                          └─── Datagram 3 ───►│
        │                   │                                 (Fire & Forget)
        │(Data Transfer...) │
```

| Parameter | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection Type** | Connection-oriented (Handshake required) | Connectionless (No handshake) |
| **Reliability** | Guaranteed delivery via Retransmissions | Unreliable (Packets can be dropped/lost) |
| **Ordering** | Guarantees sequential order of arrival | Packets may arrive out of order |
| **Flow Control** | Uses Sliding Window mechanism | None |
| **Header Size** | 20 to 60 bytes | 8 bytes |
| **Primary Use Cases** | Web Traffic (HTTP/HTTPS), Email (SMTP), File Transfer (FTP) | Video Streaming, Online Gaming, DNS Queries, VoIP |

#### The TCP 3-Way Handshake
Before any HTTP data can be transferred over TCP, a reliable socket connection must be established:
1. **SYN (Synchronize)**: Client sends a TCP segment with `SYN=1` and an initial sequence number $X$.
2. **SYN-ACK (Synchronize-Acknowledge)**: Server acknowledges with `ACK=X+1` and sends its own initial sequence number $Y$ (`SYN=1`).
3. **ACK (Acknowledge)**: Client responds with `ACK=Y+1`. The connection state becomes **ESTABLISHED**.

---

### 2.4 Domain Name System (DNS) Resolution

Human-readable domain names (e.g., `www.example.com`) must be mapped to machine-readable IP addresses (e.g., `93.184.216.34`) through the hierarchical DNS lookup system.

```
                                  +---------------------+
                                  |   Root DNS Server   |
                                  |         ( . )       |
                                  +----------▲----------+
                                             │ 2. Returns .com NS
                                 1. Query    │
                                 "example.com"
+--------------+               +-------------┴-------+
|  Client /    |──────────────►|    DNS Recursive    |
| Web Browser  |◄──────────────|      Resolver       |
+--------------+ 8. IP Address +-------------▲-------+
                  93.184.216.34              │ 4. Returns example.com NS
                                 3. Query    │
                                 "example.com"
                                  +----------▼----------+
                                  |   TLD DNS Server    |
                                  |       ( .com )      |
                                  +---------------------+
                                             │
                                 5. Query    │ 6. Returns IP
                                 "example.com" 93.184.216.34
                                  +----------▼----------+
                                  |  Authoritative NS   |
                                  |  (example.com NS)   |
                                  +---------------------+
```

#### The 4-Step DNS Hierarchy Execution:
1. **DNS Recursive Resolver**: Usually managed by an ISP or public provider (e.g., Google `8.8.8.8` or Cloudflare `1.1.1.1`). It handles the recursive lookup process for the client.
2. **Root Name Server (`.`)**: Directs the resolver to the appropriate Top-Level Domain (TLD) server based on the extension (`.com`, `.org`, `.edu`).
3. **TLD Name Server (`.com`)**: Stores registry information for specific extensions and points the resolver to the Authoritative Name Server hosting the domain records.
4. **Authoritative Name Server**: The final source of truth containing the actual DNS Mapping Records (A Record, AAAA Record, CNAME). Returns the IP address to the resolver.

---

## Module 3: The World Wide Web & HTTP Architecture

### 3.1 Anatomy of a Uniform Resource Locator (URL)

A **URL** is a specific type of **URI (Uniform Resource Identifier)** that specifies where a web resource is located and the protocol used to access it.

```
  https :// www.example.com : 8080 / courses / html / index.html ? student_id=101 # lesson2
  └─┬─┘     └──────┬──────┘   └┬─┘  └─────────────┬───────────┘ └───────┬──────┘ └───┬───┘
Protocol         Domain      Port            Path               Query String     Fragment
```

* **Protocol / Scheme**: `https://` — The rules governing communication.
* **Domain Name**: `www.example.com` — Human-readable address mapped via DNS.
* **Port**: `:8080` — Target application channel (defaults to `80` for HTTP, `443` for HTTPS if omitted).
* **Path**: `/courses/html/index.html` — Server file or route directory structure.
* **Query String**: `?student_id=101` — Key-value parameters passed to the server (`?key=value&key2=value2`).
* **Fragment / Anchor**: `#lesson2` — Client-side positioning marker (never sent to the web server).

---

### 3.2 Web Browsers & Internal Rendering Engine

A **Web Browser** is a software application designed to fetch, parse, render, and execute web resources.

```
                               BROWSER RENDERING PIPELINE
                               
┌────────────┐       ┌────────────┐
│ HTML Doc   │──────►│  DOM Tree  │──────┐
└────────────┘       └────────────┘      │
                                         ▼
                                  ┌─────────────┐     ┌──────────┐     ┌─────────┐
                                  │ Render Tree │────►│ Layout   │────►│ Paint   │
                                  └─────────────┘     └──────────┘     └─────────┘
                                         ▲
┌────────────┐       ┌────────────┐      │
│ CSS Sheet  │──────►│ CSSOM Tree │──────┘
└────────────┘       └────────────┘
```

#### Steps in the Critical Rendering Path:
1. **DOM Tree Construction**: Parses raw HTML bytes into tokens, nodes, and builds the **Document Object Model (DOM)** tree.
2. **CSSOM Tree Construction**: Parses raw CSS rules into the **CSS Object Model (CSSOM)** tree.
3. **Render Tree Generation**: Combines visible DOM nodes with CSSOM rules (elements with `display: none` are excluded).
4. **Layout (Reflow)**: Calculates exact geometric coordinates and pixel dimensions for each node on the viewport screen.
5. **Paint (Rasterization)**: Fills in pixels on screen including colors, text, borders, images, and shadows.

---

### 3.3 HTTP Request-Response Messages

#### 1. Anatomy of an HTTP Request
An HTTP Request is a structured plain-text message sent from a client to a server.

```http
GET /courses/index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: en-US,en;q=0.9
Connection: keep-alive

```

##### Structural Components:
* **Request Line**:
  * **HTTP Method**: `GET`
  * **Target Path**: `/courses/index.html`
  * **Protocol Version**: `HTTP/1.1`
* **Request Headers**: Key-value pairs providing context metadata (`Host`, `User-Agent`, `Accept`, `Authorization`, `Cookie`).
* **Blank Line**: An empty CRLF (`\r\n`) line separating headers from the payload.
* **Request Body**: Data sent to server (used in `POST`, `PUT`, `PATCH` operations; empty for `GET`).

#### Common HTTP Request Methods:

| Method | Idempotent | Safe | Purpose / Function |
| :--- | :--- | :--- | :--- |
| **`GET`** | Yes | Yes | Retrieve data from the server without modifying server state. |
| **`POST`** | No | No | Submit data to be processed by the server (creates new resources). |
| **`PUT`** | Yes | No | Completely replace a target resource with the request payload. |
| **`PATCH`** | No | No | Apply partial modifications to a resource. |
| **`DELETE`**| Yes | No | Delete the specified resource from the server. |

---

#### 2. Anatomy of an HTTP Response
An HTTP Response is the message returned by the server containing requested content or diagnostic status.

```http
HTTP/1.1 200 OK
Date: Mon, 22 Sep 2026 10:00:00 GMT
Server: Nginx/1.24.0
Content-Type: text/html; charset=UTF-8
Content-Length: 128
Connection: keep-alive

<!DOCTYPE html>
<html lang="en">
<head><title>Home Page</title></head>
<body><h1>Welcome to Web Engineering</h1></body>
</html>
```

##### Structural Components:
* **Status Line**:
  * **Protocol Version**: `HTTP/1.1`
  * **Status Code**: `200`
  * **Reason Phrase**: `OK`
* **Response Headers**: Metadata provided by server (`Server`, `Content-Type`, `Content-Length`, `Set-Cookie`).
* **Blank Line**: Empty CRLF separator.
* **Response Body**: The requested resource payload (HTML, JSON, CSS, image binary).

#### Standard HTTP Response Status Codes:

```
+-----------------------------------------------------------------------+
|  1xx INFORMATIONAL  │  100 Continue, 101 Switching Protocols          |
|  2xx SUCCESS        │  200 OK, 201 Created, 204 No Content             |
|  3xx REDIRECTION    │  301 Moved Permanently, 302 Found, 304 Not Mod. |
|  4xx CLIENT ERROR   │  400 Bad Request, 401 Unauth, 403 Forb, 404 N/F |
|  5xx SERVER ERROR   │  500 Internal Error, 502 Bad GW, 503 Service Un. |
+-----------------------------------------------------------------------+
```

---

## Module 4: The Complete 10-Step Website Working Mechanism

When a user types `https://www.example.com` into a web browser address bar and presses **Enter**, the following 10-step process occurs end-to-end:

```
[Browser] ──(1. Parse URL)──► [Local Cache Check] ──(2. Cache Miss)──► [DNS Resolver]
                                                                            │
                                                                 (3. Resolves IP)
                                                                            ▼
[Server] ◄──(5. SSL/TLS)─── [TCP 3-Way Handshake] ◄──(4. Connect IP)────────┤
   │
   ├─► (6. Process HTTP GET Request)
   │
   └───(7. Send HTTP 200 OK + HTML) ──► [Browser] ──► (8. Parse HTML/CSS)
                                                            │
                                                  (9. Fetch Sub-resources)
                                                            │
                                                  (10. Render DOM on Screen)
```

1. **URL Parsing & HSTS Check**:
   * The browser parses the scheme (`https`), domain (`www.example.com`), and port (`443`).
   * It checks its HSTS (HTTP Strict Transport Security) list to enforce HTTPS.
2. **DNS Cache Search**:
   * The browser checks local DNS caches in order: **Browser Cache** $\rightarrow$ **OS Cache** $\rightarrow$ **Router Cache** $\rightarrow$ **ISP Hosts File**.
3. **Recursive DNS Lookup** (On Cache Miss):
   * If not cached locally, a request is dispatched to the **DNS Recursive Resolver**.
   * The resolver queries Root (`.`), TLD (`.com`), and Authoritative DNS servers to get `93.184.216.34`.
4. **TCP Socket Connection**:
   * The browser initiates a TCP 3-Way Handshake (`SYN` $\rightarrow$ `SYN-ACK` $\rightarrow$ `ACK`) with `93.184.216.34` on port `443`.
5. **TLS/SSL Handshake** (Security Layer):
   * Client and Server negotiate cryptographic algorithms (Cipher Suites), exchange digital certificates, authenticate server identity, and establish encrypted session keys.
6. **HTTP Request Transmission**:
   * The browser sends an encrypted HTTP `GET / HTTP/1.1` request with headers (`Host`, `User-Agent`, `Accept`).
7. **Server Request Processing & Response**:
   * The web server (e.g., Nginx) processes the request, retrieves `index.html` from disk or application server, builds HTTP headers, and returns an `HTTP/1.1 200 OK` response payload.
8. **Document Parsing & DOM Tree Construction**:
   * The browser engine receives HTML bytes, decodes text character encoding (UTF-8), tokenizes tags, and builds the memory DOM Tree structure.
9. **Sub-resource Discovery & Parallel Requests**:
   * As the parser encounters external asset tags (`<link rel="stylesheet">`, `<script src="...">`, `<img src="...">`), it triggers secondary parallel GET requests.
10. **Layout, Paint, and Composite**:
    * The browser constructs the CSSOM, combines it with the DOM to generate the Render Tree, calculates geometry via Layout (Reflow), and paints colored pixels onto the screen.

---

## Glossary & Summary Reference

* **ARPANET**: Advanced Research Projects Agency Network — The precursor to the modern Internet.
* **Client**: An endpoint application that requests services or resources from a server.
* **Server**: A dedicated software application or computer hardware that processes requests and provides services over a network.
* **IP Address**: A unique numerical identifier assigned to every device connected to a computer network.
* **DNS**: Domain Name System — The hierarchical database that translates human-readable domain names into IP addresses.
* **TCP**: Transmission Control Protocol — A connection-oriented, reliable transport protocol guaranteeing data order and delivery.
* **UDP**: User Datagram Protocol — A connectionless, lightweight transport protocol prioritized for speed over delivery guarantees.
* **HTTP**: Hypertext Transfer Protocol — The foundation application-layer protocol for data communication on the World Wide Web.
* **DOM**: Document Object Model — An in-memory object tree representation of an HTML document structure constructed by web browsers.
