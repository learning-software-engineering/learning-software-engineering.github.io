# Software Licenses

## Table of Contents
1. [Introduction](#introduction)
2. [Why Are Software Licenses Important?](#why-are-software-licenses-important)
3. [Types of Software Licenses](#types-of-software-licenses)
    - [Public Domain](#public-domain)
    - [Permissive Licenses](#permissive-licenses)
    - [Copyleft Licenses](#copyleft-licenses)
        - [GNU Lesser General Public Licenses](#gnu-lesser-general-public-licenses)
    - [Proprietary Licenses](#proprietary-license)
4. [How to Choose the Right License?](#how-to-choose-the-right-license)
5. [Breach of Licenses](#breach-of-licences)
6. [Conclusion](#conclusion)
7. [Sources and References](#sources-and-references)


## Introduction

As software developers, it is important to know about the various licensing options that exist. A software license is a legal agreement that defines the terms under which software can be used, modified, and distributed. 


## Why Are Software Licenses Important?

Software licenses play a pivotal role in safeguarding the interests of all parties involved, from developers to end-users, ensuring lawful utilization of software. Understanding their importance is crucial for maintaining legal compliance.

### Importance of Licenses for Developers

Software licenses protect developers in various ways:

- They protect intellectual property rights by ensuring that developers have control over the software and the code they created. This prevents unauthorized use and distribution.

- They provide legal protection by clearly delimitating usage guidelines and enforcing legal boundaries. This legal framework allows developers to take legal action in case of infringement or misuse.

- They offer revenue generation as they allow developers to monetize their work through the selling of licenses.

### Importance of Licenses for Users

Softwar licenses also protect the users.

- They set permissions and restrictions for the user. In other words, these licenses define what the user can and cannot do with the software / code.

- They protect users from potential infringment claims by providing legal boundaries.

- They limit the users' legal liability.


## Types of Software Licenses

There exists multiple types of software licenses. These vary generally in terms of restrictions and permissions given to the users. Licenses typically fall into two broader categories; free and open-source licenses and proprietary licenses which are more restrictive.

### Public Domain

A public domain license is the most open type of license that exists. As its name suggests, software that belongs to the public domain is available to all. This license places no restrictions on use and distribution. Software under this license is most of the time open-source, meaning that users or other developers can freely modify its code.

### Permissive Licenses

Permissive licenses are one of the most commonly-used software licenses. They are open-source but still have minmal restrictions regarding distribution and modification. These licenses allow users substantial freedom to use, modify, and redistribute the software. These novel changes and updates do not have to be disclosed to others. In other words, developers have the right to take the software under the permissive license, modify it, add their changes, and keep the new version to themselves or share it with others. Permissive licenses allow a collaborative environment while still requiring some restrictions to be met. For instance, permissive licenses require users to include the copyright notice as well as the license text. 

Some of the popular permissve licenses are the MIT License, the Apache License, and the Berkeley Source Distribution (BSD) License.

Here is the MIT License:

Copyright (YEAR) (COPYRIGHT HOLDER)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

### Copyleft Licenses

Copyleft licenses are also known as reciprocal or restrictive licenses. A copyleft licensed code can be modified, redistributed, or incoporated in an existing proprietary project. However, these licenses require 
that the source code to all new works or adaptation are distributed under the same license. The most frequently used copyleft license in the industry is the General Public License (GPL) family of licenses. Due to their condition of making the source code of a copyleft-licensed software available to everyone, these type of licenses are not commercial-friendly. Companies do not want to share and expose their source code to other users and specifically competitiors, therefore they refrain from using software with copyleft licenses.


![GPL](https://static-assets.codecademy.com/Courses/open-source/large-software-project.svg)

#### GNU Lesser General Public Licenses

The GNU Lesser General Public License (LGPL) is a software license that is considered 'weak copyleft', meaning it imposes fewer restrictions on derivative works compared to the standard GNU General Public License (GPL). It allows developers to use LGPL-licensed libraries in their own code without necessarily having to release the source code of their own components. This is the notion of dynamic linking. For example, developers can dynamically link LGPL-licensed libraries with proprietary software without requiring the latter to be open-source. However, if modifications are made to the LGPL-licensed libraries themselves, those modifications must be released under the LGPL. This flexibility enables developers to incorporate LGPL-licensed code into both open-source and proprietary projects. While the LGPL is commonly used for software libraries and frameworks, it can also be applied to other types of software. Overlall, this type of license creates a balance between promoting openness and allowing for integration with proprietary software.

### Propietary Licenses

We have mentioned multiple times these types of licenses. To give a proper definition, prorpriatry licenses, also known as commercial licenses, are the most restrictive types of licenses. It is the opposite of free and open source licenses. Software that falls under these licenses cannot be modified or distributed to the public community. The source code is considered a trade secret. Prorpietary licenses provide the most legal protection to owners against unauthorised use of software. They fully protects the owners' inteelectual property rights. To use a software that falls under this category of licenses, users have to sign a End-User License Agreement (EULA). For instance, Microsoft Windows is a software with prorpieatry license. The latters restrics users from actions like from reverse engineering, and distributing the software to multiple users. if you do not accept the EULA, then Microsoft prevents you from using its products. 


Here is a picture summarizing the various available types of software licenses:

![Licenses](https://cdn.ttgtmedia.com/rms/onlineimages/5_types_of_software_licenses-f.png)

## How to Choose the Right License?

With so many possible options, it can be daunting to choose the license that is appropriate to your software, project, and team. 

Firstly, you should choose between the two big categories; whether you want your license to belong to the free and open source licenses or to the proprietary licenses. If you are not planning on commercializing your application, then it would be a better idea to opt for an open source license.

Among the open source licenses, if you are comfortable with someone else taking you code, changing it and making it proprietary (close), then you should go for the popular option of permissive licenses. On the other hand, if you do not want this, then using a copyleft license might be the better choice. 

For more information, check this [website](https://choosealicense.com/) created by GitHub that further explains options available to you.


## Breach of Licenses

### [Free Software Foundation, Inc. v. Cisco Systems, Inc. (2008)](https://www.fsf.org/news/2008-12-cisco-suit)

In 2008, the Free Software Foundation has filed a complaint against Cisco Sytems claiming that various Cisco products under the Linksys brand had violated the licenses of many programs on which the FSF held a copyright. Most of the programs were licensed under the GNU General Public License (GPL) and so they allowed users like Cisco to use, modify, and distribute the software in condition that the redistributors share their source code as well. The FSF accused Cisco of distirbuting licensed software without sharing source code with its customers.

The FSF and Cisco came to a settlement. You can read more about the case [here](https://www.fsf.org/news/2008-12-cisco-suit)


### [Software Freedom Conservacy and Tesla](https://www.theregister.com/2018/05/21/tesla_inches_toward_gpl_compliance/)

In 2018, after multiple years of pressure from the Software Freedom Conservacy, Tesla released part of its open-source code as required under GNU General Public Licesne (GPL). The company used some GPL-licensed software in the Tesla Model S but had failed to comply by the requiremnts of the copyleft license.

To learn more about the situation, you can read it [here](https://www.theregister.com/2018/05/21/tesla_inches_toward_gpl_compliance/)


## Conclusion

In summary, even though the world of software licenses appears to be complicated, as software developers, it is important that we are aware of these exisiting licenses. By doing so, we ensure not only compliance with legal obligations but also the safeguarding of our own rights. Understanding the nuances of different licenses allows us to work in a collaborative and responsible coding environment.

## Sources and References

- [TechTarget](https://www.techtarget.com/searchcio/definition/software-license)
- [G2 Track](https://track.g2.com/resources/software-license)
- [Indeed](https://www.indeed.com/career-advice/career-development/types-of-software-license)
- [GitHub - Choose a License](https://choosealicense.com/)
- [Synopsys](https://www.synopsys.com/blogs/software-security/5-types-of-software-licenses-you-need-to-understand.html)
- [FOSSA](https://fossa.com/blog/all-about-permissive-licenses/)
- [codecademy](https://www.codecademy.com/article/choosing-an-open-source-license)
- [Free Software Foundation, Inc. v. Cisco Systems, Inc. (2008)](https://www.fsf.org/news/2008-12-cisco-suit)
- [Software Freedom Conservacy and Tesla feud](https://www.theregister.com/2018/05/21/tesla_inches_toward_gpl_compliance/)
