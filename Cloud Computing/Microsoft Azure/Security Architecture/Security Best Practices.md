# Security Best Practices

Best practices are recommended ways to do things that have been found to be most effective or efficient. Best practices help you avoid mistakes and ensure that your resources and effort aren't wasted.

Best practices come in many forms:

1) exact instructions on what to do, why to do it, who should do it, and how to do it

2) high level principles to help with different types of decisions and actions

3) guidelines that are part of a reference architecture that describes components that should be included in a solution and how to integrate them together

Microsoft has embedded security best practices in various forms of guidance including:

1) Microsoft Cybersecurity Reference Architectures

2) Microsoft cloud security benchmark

3) the Cloud Adoption Framework (CAF)

4) the Azure Well-Architected Framework (WAF)

5) Microsoft security best practices

# Antipatterns

An antipattern is a common mistake that lead to negative outcomes. It's the opposite of a best practice. Many best practices are designed to help you avoid antipatterns.

An example of a best practice that helps you overcome numerous antipatterns is applying security patches regularly. Microsoft has observed multiple antipatterns that get in the way of regularly applying this basic and critically important security best practice:

1) We don't patch (unless it's critical) - This antipattern avoids patch installation because of an implicit assumption that patches aren't important. Another version of this is that 'It won't happen to us', a belief that unpatched vulnerabilities won't be exploited because it hasn't happened before (or hasn't been detected).

2) Waiting for patch perfection instead of building resilience - This antipattern avoids patching because of a fear that something could go wrong with the patches. This antipattern also increases likelihood of downtime from attackers.

3) Broken accountability model - This antipattern holds security accountable for the negative outcomes of patches. This accountability model leads to other teams de-prioritize security maintenance

4) Over-customizing patch selection - This antipattern uses unique criteria for patching instead of applying all manufacturer recommended patches. This customization effectively creates custom builds of Windows, Linux, and applications which have never been tested in that exact configuration.

5) Focusing only on operating systems - This antipattern patches only servers and workstations without also addressing containers, applications, firmware, and IoT/OT devices

## How architects use best practices

Security best practices must be integrated into people's skills and habits, organizational processes, and technology architecture and implementation.

Cybersecurity architects help integrate security best practices and make them actionable by doing the following:

1) Integrating best practices into security architecture and policy

2) Advising security leaders on how to integrate best practices into business processes, technical processes, and culture.

3) Advising technical teams on implementing best practices, and which technology capabilities make best practices easier to implement.

4) Advising others in the organization such as Enterprise Architects, IT Architects, application owners, developers, and more on how to integrate security best practices in their areas of ownership.

Follow best practices unless you have a reason to avoid them. Organizations should follow well-defined and well-reasoned best practices unless there is a specific reason to avoid them. While some organizations can ignore certain best practices for good reasons, organizations should be cautious before ignoring high quality best practices like those provided by Microsoft. Best practices aren't perfectly applicable to all situations, but they've been proven to work elsewhere so you shouldn't ignore or alter them without good reason.

Adapt but don't over-customize - Best practices are general guidance that work across most organizations. You may need to adapt best practices to the unique circumstances of your organization. You should be careful not to customize them to the point where the original value is lost. An example of this is adopting passwordless and multi-factor authentication, but making exceptions for the highest impact business and IT accounts that attackers value most.

Adopting best practices will reduce common mistakes and improve overall security effectiveness and efficiency. The following diagram summarizes important antipatterns and best practices.

![image](https://github.com/user-attachments/assets/8ffd9fd4-d91a-45df-86b6-701e71b888b8)

