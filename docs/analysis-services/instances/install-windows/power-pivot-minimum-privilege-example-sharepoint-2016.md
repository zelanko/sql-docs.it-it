---
title: Power Pivot con privilegi minimi esempio - SharePoint 2016 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eac736994b104ffbce855fa1ad6761d592fccad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209480"
---
# <a name="power-pivot-minimum-privilege-example---sharepoint-2016"></a>Power Pivot con privilegi minimi esempio - SharePoint 2016
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Questo argomento illustra una configurazione di esempio di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2016 con privilegi minimi. Nella configurazione viene utilizzato un account diverso per ognuno dei tre componenti e ogni account dispone del livello minimo di privilegi.  
  
## <a name="summary-of-accounts"></a>Riepilogo degli account  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2016 supporta l'uso dell'account Servizio di rete per l'account del servizio Analysis Services. L'account Servizio di rete non è supportato con SharePoint 2010. Per altre informazioni sugli account di servizio, vedere [configurare gli account del servizio Windows e le autorizzazioni](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (http://msdn.microsoft.com/library/ms143504.aspx).  
  
 Nella tabella seguente sono riepilogati i tre account utilizzati nell'esempio di configurazione con privilegi minimi.  
  
|Ambito|NOME|  
|-----------|----------|  
|Account amministratore di SharePoint|**SPAdmin**|  
|Account farm SharePoint|**SPFarm**|  
|Account del servizio Analysis Services|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>Account amministratore di SharePoint (SpAdmin)  
 **SPAdmin** è un account di dominio usato per installare e configurare la farm. È l'account usato per eseguire la Configurazione guidata SharePoint e lo strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2016. L'account **SPAdmin** è l'unico per il quale sono richiesti i diritti di amministratore locale. Prima di eseguire lo strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , concedere i privilegi dell'account **SPAdmin** all'istanza di database di SQL Server in cui vengono creati i database del contenuto e di configurazione con SharePoint. Per configurare l'account SPAdmin in uno scenario con privilegi minimi, l'account deve essere un membro dei ruoli **securityadmin** e **dbcreator**.  
  
### <a name="the-farm-account-spfarm"></a>Account farm (SPFarm)  
 **SPFarm** è un account di dominio usato dal servizio Timer di SharePoint e dall'applicazione Web per Amministrazione centrale per accedere al database del contenuto di SharePoint. Per questo account non è necessario essere un amministratore locale. Tramite la Configurazione guidata SharePoint vengono concessi i privilegi minimi appropriati nel database back-end di SQL Server. La configurazione di privilegi minimi di SQL Server è l'appartenenza ai ruoli **securityadmin** e **dbcreator**.  
  
### <a name="the-service-account-for-power-pivot-service-spsvc"></a>Account del servizio per il servizio Power Pivot (SPsvc)  
 Se una nuova farm di SharePoint non viene configurata prima dell'esecuzione dello strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , per impostazione predefinita [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] creerà gli elementi seguenti:  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Applicazione di servizio.  
  
-   Applicazione di archiviazione sicura.  
  
 Lo strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] configura entrambe le applicazioni di servizio nel pool di applicazioni predefinito. Il pool di applicazioni è in genere configurato per l'esecuzione come account SPFarm che ha accesso a numerose risorse non richieste da un account del servizio. Per impostare l'ambiente come ambiente con privilegi minimi, configurare un nuovo account di dominio che deve essere usato dal pool di applicazioni e dall'applicazione Web appropriati.  
  
 **Per creare un nuovo account di dominio SPsvc da utilizzare come account del servizio SharePoint:**  
  
1.  In Amministrazione centrale SharePoint selezionare **Sicurezza**.  
  
2.  Selezionare **Configura account di servizio**  
  
3.  Selezionare **Registra nuovo account gestito**.  
  
 L'account **SPSvc** non include i privilegi di amministratore locale e SPsvc non avrà alcun privilegio nel database di SharePoint. Gli unici privilegi richiesti da SPsvc sono i diritti di amministratore per l'istanza di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] di Analysis Services.  
  
 **Per configurare il pool di applicazioni appropriato per l'utilizzo dell'account SPsvc:**  
  
1.  In Amministrazione centrale SharePoint selezionare **Sicurezza**.  
  
2.  Selezionare **Configura account di servizio**.  
  
3.  Selezionare il pool di applicazioni del servizio usato dall'applicazione di servizio [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Successivamente, selezionare l'account SPSvc.  
  
 **Per concedere l'accesso all'applicazione Web con PowerShell:**  
  
1.  Eseguire la shell di gestione di SharePoint 2016 con privilegi di amministratore.  
  
2.  Eseguire il codice PowerShell riportato di seguito:  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
