index.html
Au début de l'année
A
Vous avez modifié 1 élément.
30 avr.
HTML
index.html
A
Vousavez créé et partagé un élément dans
21 avr.
Dossier Google Drive
MSPL4SOA
Éléments créés :
HTML
index.html
B
Modification autorisée
Bechir Zalila
Consultation autorisée
Tout le monde

<!doctype html>
<html>
<head>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
</script>
<script type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

<style>
.fTable {float: left; margin-right: 40px;}
.fClear {float: clear; }
</style>
<link rel="stylesheet" href="css/foundation.css" />
</head>
<!-- START of Markdown -->
<xmp theme="united" style="display:none;">

#MSPL4SOA tool

##Introduction
        
 The MSPL4SOA is a tool that combines the Multiple Sofware Product Line (MSPL) with the Service Oriented Architecture (SOA) paradigms. The goal of the tool is to design a $MSPL\_{SOA}$ that includes two dependent SPLs, named $SPL\_{SP}$ and  $SPL\_{SC}$, for respectively the Service Providers (SPs) and Service Consumers (SCs). These SPLs are used to generate valid and consistent SPs and SCs. 
 The MSPL4SOA tool (see Figure 1) is mainly based on the Java EE technologies and the FAMILIAR tool (https://github.com/FAMILIAR-project/familiar-documentation).
 It is composed of two generators allowing to generate customized, valid and consistent SPs and SCs, namely: `spgenerator` and `scgenerator`.

<!-- We note that the implementation of our update operator is integrated in the `spgenerator`. The goal of the update operator is to update a FM, named $FM\_{toUpdate}$, in a way so it can 
preserve (i.e., respect) all the constraints and dependencies of a given set of features denoted $F\_{preserve}$
presented in another FM, named $FM\_{toPreserve}$. -->

<figure>
<img src="./../../MSPL4SOA/img/tool_site.png" alt="tool_site" />
<figcaption><b>Figure 1: </b> Snapshots of our tool MSPL4SOA</figcaption>
</figure>

 ##The Feature Models of the Service Provider and Service Consumer

We propose to integrate in our tool practical $FM\_{SP}$ and $FM\_{SC}$ to handle the variability of $SPL\_{SP}$ and $SPL\_{SC}$.
These two FMs are respectively illustrated in the following figures.
A technical report about the features of these FMs can be downloaded
from <a href="./../../MSPL4SOA/files/fms_sc_sp.pdf">here</a> (2OO Ko).

<figure>
<img src="./../../MSPL4SOA/img/fm_spf2.png" alt="fm_sp" />
<figcaption><b>Figure 2: </b>Feature model $FM\_{SP}$</figcaption>
</figure>

---

<figure>
<img src="./../../MSPL4SOA/img/fm_scf2.png" alt="fm_sc" />
<figcaption><b>Figure 3: </b>Feature model $FM\_{SC}$</figcaption>
</figure>

##Requirements

We provide <a href="./../../tools/MSPL4SOA/files/jbdevstudio9.0.rar">here</a> a pre-configured Eclipse version (http://www.jboss.org/products/devstudio/overview/) named JbdevStudio9.0 (996 Mo) that includes all the required technologies and configurations for our tool, such:

- The ESB Switchyard2 (http://switchyard.jboss.org), that contains: HornetQ JMS (MOM implementation), Apache Camel, RestEasy, Apache CXF, ... .
- The server JBoss Enterprise Application Platform (EAP) 6.4 (http://www.jboss.org/products/eap/overview).

The `spgenerator` can be downloaded from <a href="./../../tools/MSPL4SOA/files/spgenerator.rar">here</a> (161 Mo) and the `scgenerator` can be downloaded from <a href="./../../tools/MSPL4SOA/files/scgenerator.rar">here</a> (151 Mo). 

##Getting started

<p>We provide in the following two videos that explain how our tool MSPL4SOA works. The first video presents the functionalities of the SP generator.
The second video discusses the functionalities of the SC generator</p>
     

<div class="row columns">
<div class="large-6 columns" >
<iframe  width="95%" height="425" src="https://www.youtube.com/embed/IvZQEKfGLSg" frameborder="0" allowfullscreen></iframe>
</div>

<div class="large-6 columns" >
<iframe  width="95%" height="425" src="https://www.youtube.com/embed/xmCYOrxXBXk" frameborder="0" allowfullscreen></iframe>
</div>
</div>

##Service Provider generator

The SP generator, named `spgenerator`, is an implementation of the $SPL_{SP}$ and thus responsible to generate customized SPs which are based on the
Switchyard 2 ESB.
The Switchyard 2 is a recent free software ESB developed by the Redhat company.
It adopts in its implementation the Service Component Architecture (SCA) that provides a technology-neutral assembly capability allowing
the composition of services which are developed using different technologies, such as: JMS, SOAP, REST and Apache Camel. 
These technologies have been integrated, on demand, in the generated SPs.
The SCA also separates the development of the services from that of the communication technologies.
The generated SPs can be deployed and executed in the server JBoss Enterprise Application Platform (EAP).
We also integrate the FAMILIAR tool (https://github.com/FAMILIAR-project/familiar-documentation) in the SP generator to implement our update operator
and to perform some other operations to edit FMs.
FAMILIAR is a recent tool which implements many composition (e.g., the merge by intersection) and decomposition (e.g., the slice operator) operators that can be applied to edit FMs.

The SP generator works as follows.
First, the SP developer defines the required count of services, capabilities, input and output data of his/her SP.
Given these information, the $FM\_{SP}$ and $FM\_{SC}$ will be updated as illustrated in Figures 2 and 3.
Second, he/she specializes from  $FM\_{SP}$ a $FM\_{SP\_{specialize}}$ as described in our approach.
Third, we rely on the Apache Velocity (http://velocity.apache.org/) tool as a Model To Text (M2T) template engine
to transform the $FM\_{SP\_{specialize}}$, which is defined with the FAMILIAR language (extension .fml), to source code (Java and XML files).
We ensured to highlight explicitly the places that should be modified by the SP developer in the code of SP by adding <i>TODO</i> Java comments, 
such as: the place responsible of checking the credentials given by SCs.
The generated SP will integrate, rather than the features of $FM\_{SP\_{specialize}}$, a REST service allowing SC developers to download
$FM\_{SC\_{update}}$ as a FAMILIAR file, named fm\_sc\_update.fml.
It also allows to download an XML file, named contract.xml, that contains information about the SP
which are not presented in $FM\_{SC\_{update}}$ and must be known by the SC
to correctly work (e.g., MOM JNDI configurations such the names of the generated asynchronous queues).
We prefer to not integrate these information in the $FM\_{SP}$ and $FM\_{SC}$ in order to make the FMs lesser complex and thus
contain only relevant features for SP and SC developers.
Another particularity of this file is that it reflects the features presented in $FM\_{SC\_{update}}$.
Hence, it would be possible to transform this XML file to a Java object, by using Java unmarshaling functionality,
and thus it would be easier to manipulate (i.e., retrieve, update, insert and delete features) the features of $FM\_{SC\_{update}}$.
We note that only the $FM\_{SC\_{update}}$ file is required to be used by the SC developers to generate a SC and the contract.xml file is used automatically 
when necessary by the SC generator (e.g. when using the MOM feature).


In order to test the efficiency of the SP generator in practical use, we use it to generate an SP that
offers 6 services and 25 capabilities.
We present in Tables 1, 2 and 3
analysis results about the generated Java source code, XML files and FM files. 
It requires a lesser than one minute to generate the artifacts of the SP and the same amount of time to generate $FM\_{SC\_{update}}$.


<div class="fTable">
<table>
	<caption><b>Table1:</b> Java code analysis</caption>
	<tr>
		<th align="left">Metric</th>
		<th align="right">#Count</th>
	</tr>
	<tr>
		<td align="left">Services</td>
		<td align="right">6</td>
	</tr>
	<tr>
		<td align="left">Capabilities</td>
		<td align="right">25</td>
	</tr>
	<tr>
		<td align="left">Capability input data average</td>
		<td align="right">5</td>
	</tr>
	<tr>
		<td align="left">Capability output data average</td>
		<td align="right">6</td>
	</tr>
	<tr>
		<td align="left">Packages</td>
		<td align="right">9</td>
	</tr>
	<tr>
		<td align="left">Classes</td>
		<td align="right">99</td>
	</tr>
	<tr>
		<td align="left">Interfaces</td>
		<td align="right">20</td>
	</tr>
	<tr>
		<td align="left">Methods</td>
		<td align="right">504</td>
	</tr>
	<tr>
		<td align="left">Fields</td>
		<td align="right">276</td>
	</tr>
	<tr>
		<td align="left">Lines of code</td>
		<td align="right">5186</td>
	</tr>
	<tr>
		<td align="left">Lines</td>
		<td align="right">6990</td>
	</tr>
	<tr>
		<td align="left"><i>TODO</i> Comments</td>
		<td align="right">88</td>
	</tr>
	<tr>
		<td align="left">Characters</td>
		<td align="right">211910</td>
	</tr>
	<tr>
		<td align="left">Maven dependencies Jar files</td>
		<td align="right">125</td>
	</tr><tr>
		<td align="left">JRE system library Jar files</td>
		<td align="right">16</td>
	</tr>
</table>
</div>

<div class="fTable">
<table class="bodyTable">
	<caption><b>Table 2: </b> XML code analysis</caption>
	<tr>
		<th align="left">XML File</th>
		<th align="right">#File count</th>
		<th align="right">#Line count</th>
	</tr>
	<tr>
		<td align="left">WSDL files</td>
		<td align="right">6</td>
		<td align="right">1276</td>
	</tr>
	<tr>
		<td align="left">HornetQ configuration files</td>
		<td align="right">6</td>
		<td align="right">282</td>
	</tr>
	<tr>
		<td align="left">beans.xml</td>
		<td align="right">1</td>
		<td align="right">6</td>
	</tr>
	<tr>
		<td align="left">switchyard.xml (SCA)</td>
		<td align="right">1</td>
		<td align="right">398</td>
	</tr>
	<tr>
		<td align="left">pom.xml (Maven)</td>
		<td align="right">1</td>
		<td align="right">60</td>
	</tr>
	<tr>
		<td align="left">contract.xml</td>
		<td align="right">1</td>
		<td align="right">1502</td>
	</tr>
	<tr>
		<td align="left">#Total</td>
		<td align="right">16</td>
		<td align="right">3524</td>
	</tr>
</table>

<table class="bodyTable">
	<caption><b>Table 3: </b> FM features analysis</caption>
	<tr>
	    <th align="left" rowspan="2" style="vertical-align:middle">FM File</th>
		<th align="left" colspan="3"><center>Features</center></th>
		<th align="right" rowspan="2" style="vertical-align:middle">#AMs</th>
	</tr>
	<tr>
		<th align="right">#Internal</th>
		<th align="right">#Shared</th>
		<th align="right">#Total</th>
	</tr>
	<tr>
		<td align="left">fm_sp.fml</td>
		<td align="right">172</td>
		<td align="right">947</td>
		<td align="right">1119</td>
		<td align="right">5760</td>
	</tr>
	<tr>
		<td align="left">fm_sp_specialize.fml</td>
		<td align="right">120</td>
		<td align="right">853</td>
		<td align="right">973</td>
		<td align="right">189</td>
	</tr>
	<tr>
		<td align="left">fm_sc.fml</td>
		<td align="right">335</td>
		<td align="right">947</td>
		<td align="right">1282</td>
		<td align="right">52111</td>
	</tr>
	<tr>
		<td align="left">fm_sc_update.fml</td>
		<td align="right">313</td>
		<td align="right">853</td>
		<td align="right">1166</td>
	    <td align="right">2824</td>
	</tr>
</table>
</div>

<div class="fTable" />

##Service Consumer generator

The SC generator, named `scgenerator`, consists of an implementation of the $SPL\_{SC}$ that allows to generate customized
SCs as standalone Java programs that invoke the capabilities offered by the SP.
For this purpose, two main steps are required.
First, the SC developer defines the host name of the SP to communicate with. Then, the SC generator will download, from this SP,
the $FM\_{SC\_{update}}$ and contract.xml files. The latter will be used by the SC generator to generate the input and output 
classes used by the capabilities of the SP.
Second, he/she derives from $FM\_{SC\_{update}}$ one or many $AM\_{SC\_{update}}$ as described in our approach.
Each $AM\_{SC\_{update}}$ regroups the required features to invoke a certain capability.
Afterwards, the SC generator will use the Apache Velocity tool to transform the $AM\_{SC\_{update}}$,
defined with the FAMILIAR language, to the source code of the required SC.
For each $AM\_{SC\_{update}}$, the generator generates a source code based on our Java API, 
that we propose in the following Figure, allowing to execute the $AM\_{SC\_{update}}$
at runtime. This means that the mapping between the features of the $AM\_{SC\_{update}}$ and the artifacts of SC is done at runtime.


```
       try {
          AMGenerator amGenerator = new AMGenerator("./files/am_sc_update.fml");//1

          amGenerator.start(); //2
          // If the response handler feature in your am_sc_update.fml is asynchronous, 
          // then, the code here is executed in parallel with the capability invocation.
          amGenerator.stop(); //3

          Object result = amGenerator.getResponse(); //4
          String state = amGenerator.getState(); //5
          
          } catch (AMGeneratorException e) { //6
        }
```


The API is composed of, but not limited to, six principle instructions that are required to execute an $AM\_{SC\_{update}}$. The first instruction
defines the path of the ``$AM\_{SC\_{update}}$ to execute'' in the constructor of the object AMGenerator.
The second instruction executes the $AM\_{SC\_{update}}$, i.e., it maps the features of $AM\_{SC\_{update}}$ with the artifacts of SC. 
The third instruction allows to release the resources (e.g., close the MOM connections). 
It also allows to retrieve the asynchronous responses of SOAP and REST sent from the SP. 
The SC developer can integrate some source codes between the third and fourth instructions. This code will be 
executed in parallel with the capability invocation only if the Response handler feature (see <a href="#figure2">Figure 2</a>)
presented in the $AM\_{SC\_{update}}$ is asynchronous.
The fourth instruction is used 
to retrieve the SP response (if any). The fifth instruction allows to get the state data (if any) sent from the SP. 
The sixth instruction helps to handle the exceptions thrown in case of error (e.g., unavailable service).


Many advantages can be identified when using our API. It permits to use the same code to execute the different 
$AM\_{SC\_{update}}$ independently of their features (e.g., SOAP, REST, MOM). It allows to hide the implementation
complexities of the features of $AM\_{SC\_{update}}$ by using the same interface with only few lines of code. Hence, the engineer does not require 
to work directly with the low level APIs of the features of $AM\_{SC\_{update}}$. It also allows to change the features of $AM\_{SC\_{update}}$ used to 
invoke a capability at runtime. For example, given certain reasons (e.g., the SOAP protocol is slow or not more available),
we can switch from using SOAP to REST by 
selecting the required REST features and deselecting the SOAP features from the corresponding $AM\_{SC\_{update}}$.
This can be useful, as an instance, to adapt the SC with the SP changes.
This can promote the business technology and business alignment between the SC and SP.


##Contributors

- Akram KAMOUN (<akram.kamoun@redcad.org>)
- Mohamed HADJ KACEM (<mohamed.hadjkacem@isimsf.rnu.tn>)
- Ahmed HADJ KACEM (<ahmed.hadjkacem@fsegs.rnu.tn>)
- Khalil DRIRA (<khalil@laas.fr>)



</xmp>
<!-- END of Markdown -->

<script src="http://strapdownjs.com/v/0.2/strapdown.js"></script>
</html>

