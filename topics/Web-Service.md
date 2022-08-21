# *

## table of contents

- [SOAP?](#soap)
- [* xml](#xml-hell)
- [related library (java)](#library)
- [Open API?](#open-api)
- [others](#others)

[web service](https://en.wikipedia.org/wiki/Web_service) 是一种服务导向架构的技术，通过标准的 Web 协议提供服务，目的是保证不同平台的应用服务可以互操作 ... 目前基于 Java 的主流 Web 服务开发框架往往需要 WSDL 实现客户端的源代码生成 ..

Web 服务实际上是一组工具，并有多种不同的方法调用之。三种最普遍的手段是

- 远程过程调用（RPC）Web 服务提供一个分布式函数或方法接口供用户调用，这是一种比较传统的方式。通常，在 WSDL 中对 RPC 接口进行定义（类似于早期的 XML-RPC）; (过于紧密之耦合性, RPC 式 WEB服务实质上是利用一个简单的映射，以把用户请求直接转化成为一个特定语言编写的函数或方法)

- 服务导向架构（SOA）通讯由消息驱动，而不再是某个动作（方法调用）。这种 WEB 服务也被称作面向消息的服务 ; 作为与 RPC 方式的最大差别，SOA 方式更加关注如何去连接服务而不是去实现某个特定的细节。WSDL 定义了联络服务的必要内容

- 以及表述性状态转移（Representational state transfer）Web 服务类似于 HTTP 或其他类似协议，它们把接口限定在一组广为人知的标准动作中

## soap

**SOAP** (formally an acronym for Simple Object Access Protocol 简单对象访问恊定") 是交换数据的一种协议规范，使用在计算机网络 Web 服务（web service）中，交换带结构的信息。基于 XML 的可扩展消息信封格式，需同时绑定一个网络传输协议。Some concepts: [check also](https://en.wikipedia.org/wiki/SOAP)

- SOAP envelope 定义了一个框架，描述消息中的内容是什么、是谁发送的、谁应当接受并处理它以及如何处理它们
- SOAP encoding rules 定义了一种序列化的机制，用于表示应用程序需要使用的数据类型的实例
- SOAP RPC representation 定义了一个协定，用于表示远程过程调用和应答
- SOAP binding 定义了 SOAP 使用哪种协议交换信息。使用 HTTP/TCP/UDP 协议都可以
- **etc**

**WSDL (Web Service Description Language)** 一个 XML 格式文档，用以描述服务端口访问方式和使用协议的细节。通常用来辅助生成服务器和客户端代码及配置信息以供调用。此类 WEB 服务关注与那些稳定的资源的互动，而不是消息或动作 ; 此种服务可以通过 WSDL 来描述 SOAP 消息内容，通过 HTTP 限定动作接口；或者完全在 SOAP 中对动作进行抽象

---

What is SOAP MTOM? [more info](https://www.ibm.com/support/knowledgecenter/en/SSMKHH_9.0.0/com.ibm.etools.mft.doc/ac56620_.htm)

- SOAP Message Transmission Optimization Mechanism (**MTOM**) is the use of MIME to optimize the bitstream transmission of SOAP messages that contain significantly large base64Binary elements.

- The MTOM message format allows bitstream compression of binary data. Data that would otherwise have to be encoded in the SOAP message is instead transmitted as raw binary data in a separate MIME part. A large chunk of binary data takes up less space than its encoded representation, so MTOM can reduce transmission time, although it can increase processor usage.

- An MTOM message is identified by a Content-Type with a type of `application/xop+xml`

---

SOAP is less "simple" than the name would suggest. The verbosity of the protocol, slow parsing speed of XML, and lack of a standardized interaction model led to the dominance of services using the HTTP protocol more directly. E.g., [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)

## XML Hell

Extensible Markup Language (XML) defines a set of rules for encoding documents in a format that is both human-readable and machine-readable.

The design goals of XML emphasize simplicity, generality, and usability across the Internet. Although the design of XML focuses on documents, the language is widely used for the representation of arbitrary _data structures_ such as those used in _web services_.

**XML schema** 是指各种 XML 文档（称作schema），用于表示在 XML 一般规则之外的特定文档的结构与内容的约束。其中被 W3C 采纳为推荐标准的 schema 语言是 XSD.

There are languages developed specifically to express XML schemas, e.g., DTD (document type definition)

> xml declaration should precede all document content (space !)

## library

- Axis (Apache eXtensible Interaction System); **Apache Axis2** (a complete re-design and re-write of the widely used Apache Axis SOAP stack) 是一个 Web 服务的核心支持引擎，是一个 SOAP 的实现

- **Axiom** stands for _Axis Object Model_ and refers to the XML infoset model that is initially developed for Apache Axis2. XML infoset refers to the information included inside the XML, and for programmatic manipulation it is convenient to have a representation of this XML infoset in a language specific manner.

- _StAX (JSR 173)_ is the standard pull parser API for Java.

- _Apache CXF_ (Celtix + XFire) is an open source services framework. It helps you build and develop services using frontend programming APIs, like JAX-WS and JAX-RS. It supports a variety of web service standards.

- Servlet (Server Applet) 是用 Java 编写的服务器端程序, 其主要功能在于交互式地浏览和修改数据，生成动态 Web 内容; 广义的 Servlet 是指任何实现了这个 Servlet 接口的类; life cycle of a servlet (central part: `init()`, `service()`, `destroy()`): guess what

- JAX-RS (JSR 311) is a specification for implementing REST web services in Java, currently defined by the JSR-370.

## Open API

An open API (often referred to as a public API) is a publicly available _application programming interface_ that provides developers with programmatic access to a proprietary software application or web service.

### in business

Yahoo's open search API allows developers to integrate Yahoo search into their own software applications.

With respect to Facebook and Twitter, we can see how third parties have enriched these services with their own code. For example, the ability to create an account on an external site/app using your Facebook credentials is made possible using Facebook's open API.

### on the web

Some open APIs fetch data from the database behind a website and these are called Web APIs. For example, Google's YouTube API allows developers to integrate YouTube into their applications by providing the capability to search for videos, retrieve standard feeds, and see related content.

## others

Multipurpose Internet Mail Extension (MIME) is an _Internet standard_ that extends the format of email messages to support text in character sets other than ASCII, as well as attachments of audio, video, images, and application programs.

The **Web Service Interoperability Organization (WS-I)** was an industry consortium. WS-I did not define standards for web services; rather, it creates guidelines and tests for interoperability.

[back to top](#table-of-contents)

### links

- [JAX-RS and Spring Rest](https://stackoverflow.com/questions/42944777/difference-between-jax-rs-and-spring-rest)
- No message body writer found for class - automatically mapping non-simple resources [check](https://stackoverflow.com/questions/6312030/cxf-no-message-body-writer-found-for-class-automatically-mapping-non-simple-r)
- [check also](https://stackoverflow.com/questions/2728495/what-is-the-difference-between-java-rmi-and-rpc)
