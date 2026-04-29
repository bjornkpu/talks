Introduction to

# Model Context Protocol (MCP)

**Bridging LLMs and Backend Systems**

> Bjørn Kristian Punsvik. 04-04-2025

---

### Objective of the Presentation

- What MCP is and how it works
- The problems it solves for LLMs and developers
- The architecture and core concepts of MCP
- A practical demonstration of building an MCP server and client

---

![[MCP Presentation.png]]

**MCP Hosts**, **MCP Clients**, **MCP Servers**, **Local Data Sources**, **Remote Services**.

note:
standardize how applications provide context to Large Language Models (LLMs). bridge between LLMs and various data sources and tools. USB-C port

- Programs like Claude Desktop, IDEs, or AI tools that want to access data through MCP
- Protocol clients that maintain 1:1 connections with servers
- Lightweight programs that each expose specific capabilities through the standardized Model Context Protocol
- Your computer’s files, databases, and services that MCP servers can securely access
- External systems available over the internet (e.g., through APIs) that MCP servers can connect to

---

- **MCP Hosts**: Programs like Claude Desktop, IDEs, or AI tools that want to access data through MCP
- **MCP Clients**: Protocol clients that maintain 1:1 connections with servers
- **MCP Servers**: Lightweight programs that each expose specific capabilities through the standardized Model Context Protocol
- **Local Data Sources**: Your computer’s files, databases, and services that MCP servers can securely access
- **Remote Services**: External systems available over the internet (e.g., through APIs) that MCP servers can connect to

---

## History

---

## 2. What is MCP?

### Definition of MCP

The Model Context Protocol (MCP) is an open protocol that standardizes the way applications provide context to Large Language Models (LLMs). It defines a set of rules and structures that enable seamless communication between LLMs and various data sources, tools, and services. By establishing a common framework, MCP allows developers to build applications that can effectively leverage the capabilities of LLMs, enhancing their functionality and usability in diverse scenarios.

### Analogy: MCP as a USB-C Port for AI Applications

To better understand MCP, think of it as a USB-C port for AI applications. Just as USB-C provides a universal and standardized way to connect various devices—such as smartphones, laptops, and peripherals—MCP offers a standardized method for connecting LLMs to different data sources and tools. This analogy highlights the versatility and interoperability of MCP, allowing developers to plug in various functionalities and data sources without worrying about compatibility issues. With MCP, developers can focus on building intelligent applications rather than dealing with the complexities of integration.

### Key Features of MCP

MCP comes with several key features that make it a powerful tool for developers working with LLMs:

1. **Standardized Communication**: MCP provides a consistent protocol for communication between LLMs and external systems, ensuring that data is exchanged in a predictable manner.

2. **Integration with Tools and Resources**: MCP allows LLMs to access a wide range of tools and resources, enabling them to perform actions, fetch data, and interact with external services. This capability enhances the functionality of LLMs beyond simple text generation.

3. **Flexibility and Interoperability**: With MCP, developers can easily switch between different LLM providers and integrate various data sources without significant changes to their codebase. This flexibility fosters innovation and experimentation.

4. **Security Best Practices**: MCP incorporates best practices for securing data and ensuring that sensitive information is handled appropriately. This is crucial for applications that require compliance with data protection regulations.

5. **Growing Ecosystem**: MCP is designed to support a growing list of pre-built integrations, making it easier for developers to connect their applications to popular tools and services.

By leveraging these features, developers can create more sophisticated and context-aware applications that harness the full potential of LLMs.

---

## 3. Why MCP?

### Problems MCP Solves for LLMs

#### Integration with Data and Tools

One of the primary challenges faced by LLMs is the need to integrate with various data sources and tools to provide accurate and relevant responses. Traditional LLMs often operate in isolation, limiting their ability to access real-time information or perform specific actions. MCP addresses this issue by providing a standardized protocol that allows LLMs to seamlessly connect with external data sources, APIs, and tools. This integration enables LLMs to fetch live data, execute functions, and enhance their responses based on
