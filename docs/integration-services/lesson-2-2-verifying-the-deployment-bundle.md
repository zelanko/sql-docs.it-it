---
title: 'Passaggio 2: Verifica del pacchetto di distribuzione | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fec0b4e8180141fdea37e2ac484f5a2b0195b44a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917241"
---
# <a name="lesson-2-2---verifying-the-deployment-bundle"></a>Lezione 2-2 - Verifica del pacchetto di distribuzione

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Nella lezione 1 è stato creato il progetto Deployment Tutorial a cui sono stati aggiungi pacchetti e file ausiliari. Nell'attività precedente è stata compilata un'utilità di distribuzione per il progetto.  
  
In questa attività si procederà alla verifica dei contenuti del pacchetto di distribuzione. Quest'ultimo rappresenta la cartella che verrà copiata nel computer di destinazione e utilizzata per installare i pacchetti. Se è stato usato il valore predefinito, ovvero bin\Deployment, come percorso dell'utilità di distribuzione, il pacchetto di distribuzione si trova nella cartella Bin\Deployment all'interno della cartella Deployment Tutorial del progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>Per verificare il contenuto del pacchetto di distribuzione  
  
1.  Individuare la cartella bin\Deployment nel computer in uso.  
  
2.  Verificare che siano presenti i file seguenti:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Fare clic con il pulsante destro del mouse su Deployment Tutorial.SSISDeploymentManifest, scegliere **Apri con**, quindi fare clic su **Internet Explorer**. È inoltre possibile aprire il file in un editor di testo, ad esempio Blocco note. Il codice XML dovrebbe risultare analogo al seguente:  
  
    `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Verificare che il valore dell'attributo **AllowConfigurationChanges** sia **True** e che il codice XML includa un elemento **pacchetto** per ognuno dei due pacchetti, un elemento **MiscellaneousFile** per ognuno dei quattro file non pacchetto e un elemento **ConfigurationFile** per ognuno dei due file di configurazione XML.  
  
5.  Chiudere Internet Explorer o l'editor di testo.  
  
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 3: Installare i pacchetti SSIS](../integration-services/lesson-3-install-ssis-packages.md)  
  
  
  
