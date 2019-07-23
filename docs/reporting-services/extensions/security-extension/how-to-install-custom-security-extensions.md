---
title: Come installare estensioni di sicurezza personalizzate | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9fcef802f6c61b85b4905365bda075a9f11d9e10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68223233"
---
# <a name="how-to-install-custom-security-extensions"></a>Come installare estensioni di sicurezza personalizzate

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 ha introdotto un nuovo portale Web per ospitare le nuove API Odata e i nuovi carichi di lavoro dei report, ad esempio report per dispositivi mobili e indicatori KPI. Questo nuovo portale si basa su tecnologie più recenti e viene isolato da ReportingServicesService mediante l'esecuzione in un processo separato. Questo processo non è un'applicazione ASP.NET ospitata e interrompe i presupposti delle estensioni di sicurezza personalizzate esistenti. Inoltre, le interfacce correnti delle estensioni di sicurezza personalizzate non consentono il passaggio di contesti esterni, lasciando ai responsabili dell'implementazione l'unica scelta di controllare gli oggetti ASP.NET globale noti richiedendo alcune modifiche all'interfaccia.

## <a name="what-changed"></a>Che cosa è cambiato?

È stata introdotta una nuova interfaccia che può essere implementata e che offre un IRSRequestContext con le proprietà più comuni usate dalle estensioni per prendere decisioni relative all'autenticazione.

Nelle versioni precedenti Gestione report rappresentava il front-end e poteva essere configurato con la propria pagina di accesso personalizzata. In Reporting Services 2016 è supportata una sola pagina ospitata da ReportServer che deve eseguire l'autenticazione in entrambe le applicazioni.

## <a name="implementation"></a>Implementazione

Nelle versioni precedenti le estensioni potevano avvalersi del presupposto comune che gli oggetti ASP.NET sarebbero stati immediatamente disponibili. Poiché il nuovo portale non viene eseguito in ASP.NET, l'estensione potrebbe riscontrare problemi con gli oggetti NULL.

Nella maggior parte dei casi si accede a HttpContext.Current per leggere le informazioni della richiesta, ad esempio le intestazioni e i cookie. Per consentire alle estensioni di prendere le stesse decisioni è stato introdotto un nuovo metodo nell'estensione che offre le informazioni della richiesta e viene chiamato durante l'autenticazione dal portale. 

Per usare il nuovo metodo è necessario che le estensioni implementino l'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2>. Le estensioni dovranno implementare entrambe le versioni del metodo <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> che viene chiamato dal contesto di ReportServer e usato nel processo del webhost. Nell'esempio seguente è illustrata una delle implementazioni semplici del portale in cui l'identità risolta da ReportServer corrisponde a quella usata.

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>Distribuzione e configurazione

Le configurazioni di base necessarie per l'estensione di sicurezza personalizzata corrispondono a quelle delle versioni precedenti. È necessario apportare modifiche per web.config e rsreportserver.config: Per altre informazioni, vedere [Configurare l'autenticazione personalizzata o basata su form nel server di report](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).

Non è più disponibile un web.config separato per Gestione report. Il portale eredita le stesse impostazioni dell'endpoint di ReportServer.

## <a name="machine-keys"></a>Chiavi computer

Per l'autenticazione basata su form che richiede la decrittografia del cookie di autenticazione, è necessario configurare entrambi i processi con la stessa chiave computer e lo stesso algoritmo di decrittografia. Si tratta di un passaggio già noto a coloro hanno precedentemente configurato Reporting Services per l'uso in ambienti di scalabilità orizzontale, ma ora è un requisito anche per le distribuzioni in un singolo computer.

Usare una chiave di convalida specifica per la distribuzione. Sono disponibili diversi strumenti per la generazione delle chiavi, ad esempio Gestione Internet Information Services (IIS). Altri strumenti sono disponibili su Internet.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 e versioni successive

**\ReportServer\rsReportServer.config**

Aggiungere in `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

Aggiungere in `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

Aggiungere in `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Server di report di Power BI

Disponibile a partire dalla versione di giugno 2017 (Build 14.0.600.301).

**\ReportServer\rsReportServer.config**

Aggiungere in `<configuration>`.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>Configurare i cookie pass-through

Analogamente alla versione precedente di Gestione report, il nuovo portale e ReportServer comunicano tramite API SOAP interne per alcune operazioni. Quando è necessario il passaggio di ulteriori cookie dal portale al server, le proprietà PassThroughCookies sono ancora disponibili. Per altre informazioni, vedere [Configurare il portale Web per il passaggio di cookie di autenticazione personalizzati](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>Passaggi successivi

[Configurare l'autenticazione personalizzata o basata su form nel server di report](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Configurare Gestione report per il passaggio di cookie di autenticazione personalizzati](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
