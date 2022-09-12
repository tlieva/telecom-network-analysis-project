# Telecom Network Analysis Capstone Project

This is a repository for my self-directed capstone project done in collaboration with a telecommunication service provider based in Vancouver BC, Canada. The project was completed as part my post-graduate studies in Analytics for Business Decision-Making at George Brown College (BUS 4045	Data Project Capstone Project), where my team and I had the opportunity to work for a client in support of a data-driven business decision. 

Output of the project was structured as a series of reports and final presentation to the faculty and client through various stages of engagement with the client. 

### Objective:
My team and I aimed to provide our client a static analytical model of network telemetry data as framework for future real-time analysis for live level data integration that would provide our client a tool that would help optimize their network service recommendations to customers based on observed traffic micro-trends in improving customer services. 

This included the following **interactive dashboard** using internal network telemetry data for _network traffic categorization_, _network re-classification in reference to IANA_ (repository of network traffic based on port numbers and protocols), and _analysis of peak times in data use_. We also developed an **RFM scoring-based marketing analysis tool** for customer segmentation in identifying target customer segment based on network usage, frequency, and number of connections.

**Application(s) used:** Python, Tableau

**Project File(s):** 
- [Sample Dashboard-PDF](https://github.com/tlieva/telecom-network-analysis-project/blob/95027fdb2711fd70b8ae50e492a2074def011bcd/Network-Analysis-%20Dashboard.pdf)
- [Sample Code-PDF](https://github.com/tlieva/telecom-network-analysis-project/blob/f252bb684fc855ac6800ca92fa2a5d43ed8c0728/Network_Analytical_File_Sample_Code.pdf)

_Note: Files are in PDF format and redacted to remove identifying information_


## Summary of Methodology
Due to computational limitations, a sample dataset was obtained from the client containing only **15 minutes of network data** for analysis. 

Subsequent data exploration, cleaning, and processing was completed using Python JupyterNotebook. The purpose was to ensure that data was usable for further analysis of the network data, and creating traffic classification based on the data provided. Network traffic _re-classification_ was completed in reference to the Internet Assigned Numbers Authority (IANA) which maintains a repository of protocols and port numbers it has assigned. Further data modelling and visualization was completed in Tableau.

Based on our preliminary assessment of the data, converstions with our client, and knowledge supplemented by external research, the following source variables of interest were identified to be pertinent in achieving our objectives:
- **Time variables:** ts (time start), te (time end), td (time duration)
- **Packets:** ipkt (incoming packets), opkt (outgoing packets)
- **Bytes:** ibyt (incoming bytes), obyt (outgoing bytes)
- **Protocol:** pr (protocol)
- **Ports:** sp (source port), dp (destination port)
- **IP Address:** sa (source IP address), da (destination IP address)
- **MAC addresses:** ismc (input source mac), odmc (output destination mac), osmc (output source mac), idmc (input destination mac)

_**NOTE!** For the purpose of the project, each source IP address was defined as a unique customer in the network._

Additional **derived variables** for network analysis that were also created. This included identifying the **traffic type and code** based on source protocol and port numbers, and getting the aggregated **total of bytes** transferred in a network by each source IP and **number of connections** made for each respective customer. We also wanted to measure the **delivery ratio of the incoming bytes relative to outgoing bytes**, where an invariably high number indicates unusual behaviour, and can be flagged for analysis. A time series was created as a result to identify peak time uses for each IP address, as shown below:

<img width="1011" alt="Screen Shot 2022-07-16 at 2 53 11 AM" src="https://user-images.githubusercontent.com/106416383/179343860-bfbaef3d-5470-4b04-98db-2477a03c71ad.png">


For subsequent customer segmentation, we used a RECENY, FREQUENCY, AND MONETARY scoring approach in developing our own UFM analysis, where we looked to assign a labelled UFM score using three key variables:
1. **Usage** of network defined as the sum of total bytes used for each unique source IP
2. **Frequency** of the source IP appearing in the network
3. **Count** of connections for each source IP

Customers were then assigned a value level based on their respective quantile in which they reside in as determined by their aggregated UFMscore. Lower quantiles were classified as no value or low, top two quantiles were classified as high or medium.


#### UFM Level
The marketing segment assigned to customers based on UFMScore. 
- Lower scores were labeled 'Possible Customer Loss' or 'Needs Attention'. 
- Higher scores are labeled as 'Potential Sales' and 'Require Upgrade'.

<img width="549" alt="Screen Shot 2022-07-16 at 2 55 04 AM" src="https://user-images.githubusercontent.com/106416383/179343921-5a109bc6-83fc-4218-93d8-34e3c79cbf3c.png">

<img width="931" alt="Screen Shot 2022-07-09 at 8 05 17 PM" src="https://user-images.githubusercontent.com/106416383/178126456-4f95dde9-7daa-4b86-a2d6-9dfb5629416b.png">

## Profile of usage based on UFM level
<img width="444" alt="Screen Shot 2022-07-09 at 8 15 17 PM" src="https://user-images.githubusercontent.com/106416383/178126616-8ea35ce1-3748-44af-a96b-a674471a69f5.png">


