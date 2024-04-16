# Trees, Forest and Trust Relationships in Windows AD

### In the context of Windows Active Directory (AD), trees, forests, and trusts are fundamental concepts that define the structure and relationships within an AD environment.

1. **Trees**: In Windows AD, a tree refers to a collection of domains that share a contiguous namespace. Each domain within a tree shares a common Domain Name System (DNS) namespace and forms a hierarchy. The first domain created in a new AD forest becomes the root domain of the tree, and additional domains can be added beneath it. Domains within a tree have a hierarchical relationship, with parent-child relationships similar to the structure of a tree. Each domain in a tree has a unique name but shares a common schema and configuration partition.

2. **Forests**: A forest in Windows AD is a collection of one or more trees that share a common schema, configuration, and global catalog. Forests provide a way to organize and manage multiple trees of domains, and they establish trust relationships between these domains. Each forest has a unique identifier called the ForestRootDomain, which is the first domain created when the forest is established. All domains within a forest share the same schema and global catalog, allowing for centralized management and authentication.

3. **Trusts**: Trusts in Windows AD are relationships established between domains or forests to allow users in one domain to access resources in another domain. Trust relationships are essential for enabling users in different parts of an organization to collaborate and access shared resources. Trusts can be one-way or two-way, and they can be transitive or non-transitive. Transitive trusts flow through the trust path, allowing authentication and authorization to occur across multiple domains within a forest or across multiple forests. Non-transitive trusts are limited to the two domains involved in the trust relationship.

### Overall, trees, forests, and trusts are foundational concepts in Windows AD that define the structure, organization, and relationships within a distributed network environment, enabling centralized management and secure resource access across domains and forests.

## 2 Kinds of trust relationships

 - One-way trust relationships

 - Two-way trust relationships (Default)
