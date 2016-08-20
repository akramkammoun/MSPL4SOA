#Introduction

The MSPL4SOA is a tool that combines the Multiple Sofware Product Line (MSPL) with the Service Oriented Architecture (SOA) paradigms. The goal of the tool is to design an MSPL that includes two dependent SPLs, named SPL<SUB>SP</SUB> and  SPL<SUB>SC</SUB>, for respectively the Service Providers (SPs) and Service Consumers (SCs). These SPLs are used to generate valid and consistent SPs and SCs. 
The MSPL4SOA tool (see Figure 1) is mainly based on the Java EE technologies and the FAMILIAR tool (https://github.com/FAMILIAR-project/familiar-documentation). 
FAMILIAR is a recent tool which implements many composition (e.g., the merge by intersection) and decomposition (e.g., the slice operator) operators that can be applied to edit FMs. Our tool is composed of two generators allowing to generate customized, valid and consistent SPs and SCs, namely: `spgenerator` and `scgenerator`.

#Requirements 
We provide <a href="./files/jbdevstudio9.0.rar">here</a> a pre-configured Eclipse version (http://www.jboss.org/products/devstudio/overview/) named JbdevStudio9.0 (996 Mo) that includes all the required technologies and configurations for our tool, such:</p>
<ul>
<li>The ESB Switchyard2 (http://switchyard.jboss.org), that contains: HornetQ JMS (MOM implementation), Apache Camel, RestEasy, Apache CXF, ... .</li>
<li>The server JBoss Enterprise Application Platform (EAP) 6.4 (http://www.jboss.org/products/eap/overview).</li>
</ul>
The `spgenerator` can be downloaded from <a href="./files/spgenerator.rar">here</a> (161 Mo) and the `scgenerator` can be downloaded from <a href="./scgenerator.rar">here</a> (151 Mo).

#Getting started
We provide in the following two videos that explain how our tool MSPL4SOA works. The first video presents the functionalities of the SP generator (https://www.youtube.com/embed/IvZQEKfGLSg). 
The second video discusses the functionalities of the SC generator (https://www.youtube.com/embed/xmCYOrxXBXk).
     
#More information
Please consult the website of the tool from more information (https://akramkammoun.github.io/MSPL4SOA/). 
