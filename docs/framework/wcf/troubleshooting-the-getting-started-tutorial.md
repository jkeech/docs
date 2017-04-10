---
title: "Troubleshooting the Getting Started Tutorial | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
---
# Troubleshooting the Getting Started Tutorial
This topic lists the most common problems encountered when working through the Getting Started Tutorial and how to resolve them.  
  
1.  [I am unable to find the project files on my hard drive.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q1)  
  
2.  [Attempting to run the service application: HTTP could not register URL http://+:8000/ServiceModelSamples/Service/. Your process does not have access rights to this namespace.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q2)  
  
3.  [Attempting to use the Svcutil.exe tool: 'svcutil' is not recognized as an internal or external command, operable program or batch file.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q3)  
  
4.  [Unable to find the App.config file generated by Svcutil.exe.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q4)  
  
5.  [Compiling the client application: 'CalculatorClient' does not contain a definition for '&lt;method name&gt;' and no extension method '&lt;method name&gt;' accepting a first argument of type 'CalculatorClient' could be found (are you missing a using directive or an assembly reference?)](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q5)  
  
6.  [Compiling the client application: The type or namespace name 'CalculatorClient' could not be found (are you missing a using directive or an assembly reference?)](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q6)  
  
7.  [Running the client: Unhandled Exception: System.ServiceModel.EndpointNotFoundException: Could not connect to http://localhost:8000/ServiceModelSamples/Service/CalculatorService. TCP error code 10061: No connection could be made because the target machine actively refused it.](../../../docs/framework/wcf/troubleshooting-the-getting-started-tutorial.md#BKMK_q7)  
  
<a name="BKMK_q1"></a>   
## I am unable to find the project files on my hard drive.  
 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] saves project files in c:\users\\<user name\Documents\\<Visual Studio version\>\Projects in [!INCLUDE[wv](../../../includes/wv-md.md)] and [!INCLUDE[win7_client_secondref](../../../includes/win7-client-secondref-md.md)], and c:\Documents and Settings\\<user name\>\My Documents\\<Visual Studio version\>\Projects in earlier versions of Windows.  
  
<a name="BKMK_q2"></a>   
## Attempting to run the service application: HTTP could not register URL http://+:8000/ServiceModelSamples/Service/. Your process does not have access rights to this namespace.  
 The process that hosts a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] service must be run with Administrative privileges. If you are running the service from inside [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] you must run [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] as an Administrator. To do so click **Start**, right-click [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] and select **Run As Administrator**. If you are running the service from a command-line prompt you must start the command line prompt as an Administrator in a similar way. Click **Start**, right-click **Command Prompt** and select **Run As Administrator**.  
  
<a name="BKMK_q3"></a>   
## Attempting to use the Svcutil.exe tool: 'svcutil' is not recognized as an internal or external command, operable program or batch file.  
 Svcutil.exe must be in the system path. The easiest solution is to use the Command Prompt. Click **Start**, select **All Programs**, [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], **Visual Studio Tools**, and [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] **Command Prompt**. This command prompt sets the system path to the correct locations for all tools shipped as part of [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)].  
  
<a name="BKMK_q4"></a>   
## Unable to find the App.config file generated by Svcutil.exe.  
 The **Add Existing Item** dialog only displays files with the following extensions by default: .cs, .resx, .settings, .xsd, .wsdl. You can specify that you want to see all file types by selecting **All Files (\*.\*)** in the drop down list box in the lower right corner of the **Add Existing Item** dialog box.  
  
<a name="BKMK_q5"></a>   
## Compiling the client application: 'CalculatorClient' does not contain a definition for '\<method name>' and no extension method '\<method name>' accepting a first argument of type 'CalculatorClient' could be found (are you missing a using directive or an assembly reference?)  
 Only those methods that are marked with the `ServiceOperationAttribute` are exposed to the outside world. If you omitted the `ServiceOperationAttribute` attribute from one of the methods in the `ICalculator` interface you get this error message when compiling a client application that makes a call to the operation missing the attribute.  
  
<a name="BKMK_q6"></a>   
## Compiling the client application: The type or namespace name 'CalculatorClient' could not be found (are you missing a using directive or an assembly reference?)  
 You get this error if you do not add the Proxy.cs or Proxy.vb file to your client project.  
  
<a name="BKMK_q7"></a>   
## Running the client: Unhandled Exception: System.ServiceModel.EndpointNotFoundException: Could not connect to http://localhost:8000/ServiceModelSamples/Service/CalculatorService. TCP error code 10061: No connection could be made because the target machine actively refused it.  
 This error occurs if you run the client application without running the service.  
  
<a name="BKMK_q8"></a>   
## Unhandled Exception: System.ServiceModel.Security.SecurityNegotiationException: SOAP security negotiation with 'http://localhost:8000/ServiceModelSamples/Service/CalculatorService' for target 'http://localhost:8000/ServiceModelSamples/Service/CalculatorService' failed  
 This error occurs on a domain-joined computer that does not have network connectivity. Either connect your computer to the network or turn off security for both the client and the service. For the service, modify the code that creates the WSHttpBinding to the following.  
  
```  
// Step 3 of the hosting procedure: Add a service endpoint  
selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
  
```  
  
 For the client, change the **\<security>** element under the **\<binding>** element to be the following:  
  
```  
<security mode="Node" />  
```  
  
## See Also  
 [Getting Started Tutorial](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [WCF Troubleshooting Quickstart](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md)   
 [Troubleshooting Setup Issues](../../../docs/framework/wcf/troubleshooting-setup-issues.md)