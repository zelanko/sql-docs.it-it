---
title: Configurare la raccolta di dati di diagnostica e utilizzo per gli strumenti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c60eb8cac357fba523196385e72a1b05a2c36f4
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59243515"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-tools"></a>Configurare la raccolta di dati di diagnostica e utilizzo per gli strumenti di SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Informazioni su come il programma Analisi utilizzo software consente a Microsoft di identificare modi per migliorare il software.  È possibile configurare gli strumenti per i quali si vuole o meno partecipare in qualsiasi momento.  
  
> [!NOTE]  
> Per una spiegazione delle procedure di raccolta e di trattamento dei dati per le versioni di Microsoft SQL Server, fare riferimento a questa [informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=868444).  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>Consenso o rifiuto esplicito per la partecipazione ad Analisi utilizzo software per SQL Server Data Tools  

 Il programma Analisi utilizzo software è progettato per consentire a Microsoft di migliorare i propri prodotti nel tempo. Questo programma raccoglie informazioni sull'hardware del computer e la modalità di utilizzo del prodotto, senza interrompere gli utenti durante le attività nel computer. Le informazioni raccolte consentono a Microsoft di identificare le funzionalità da migliorare. Questo documento illustra le procedure per accettare o rifiutare in modo esplicito la partecipazione al programma Analisi utilizzo software per SQL Server Data Tools (SSDT) per Visual Studio 2017, Visual Studio 2015 e Visual Studio 2013.  

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>Scelta e controllo per il programma Analisi utilizzo software e SQL Server Data Tools per Visual Studio 2017

 SSDT per Visual Studio 2017 è lo strumento di modellazione dei dati accluso a SQL Server 2017. Usa le opzioni di Analisi utilizzo software integrate in Visual Studio 2017. In questo [documento della Guida da Visual Studio](https://www.visualstudio.com/docs/work/connect/give-feedback) sono disponibili altre informazioni sull'invio di commenti e suggerimenti con Analisi utilizzo software in Visual Studio 2017.  
  
 Nelle versioni di anteprima di SQL Server 2017 la funzionalità Analisi utilizzo software è attivata per impostazione predefinita. È possibile disattivarla o riattivarla seguendo le istruzioni seguenti.  
  
 **In Visual Studio (si applica alle installazioni complete di Visual Studio 2017)**  
  
 Se si esegue l'installazione di SSDT in un computer che dispone già di Visual Studio, vengono aggiunti solo i modelli di progetto Business Intelligence e SQL Server. In questo scenario, le opzioni per l'invio di commenti e suggerimenti offerte da Visual Studio possono essere usare per il consenso o il rifiuto esplicito per Analisi utilizzo software.  
  
1.  Avviare Visual Studio.  
  
2.  Dal menu Guida, selezionare **Invia commenti e suggerimenti** > **Impostazioni**.  
  
3.  Per disattivare Analisi utilizzo software, fare clic su **No, non desidero partecipare**, quindi fare clic su **OK**.  
  
     Per attivare Analisi utilizzo software, fare clic su **Sì, desidero partecipare al programma**, quindi fare clic su **OK**.  
  

  
 **Usare criteri basati sul Registro di sistema o Criteri di gruppo**  
  
 Se si esegue l'installazione di SSDT in un computer che non ha Visual Studio 2017, verrà installata solo la shell di Visual Studio. La shell non fornisce opzioni per i suggerimenti dei clienti. In questo caso, un aggiornamento del Registro di sistema è l'unica opzione per la configurazione di Analisi utilizzo software.  
  
 I clienti aziendali possono creare Criteri di gruppo per partecipare o meno impostando criteri basati sul Registro di sistema per SQL Server 2017.  
  
 Le relative impostazioni e chiavi del Registro di sistema sono le seguenti:  
  
- Sistema operativo a 64 bit, Chiave = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM
- Sistema operativo a 32 bit, Chiave = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM

Quando Criteri di gruppo è attivata, Chiave = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM 

Voce = OptIn

Valore = (DWORD)
- 0 è rifiutato esplicitamente (disattivare VSCEIP)
- 1 è accettato esplicitamente (attivare VSCEIP)

  
> [!CAUTION]  
>  Se il Registro di sistema viene modificato in modo non appropriato, il sistema potrebbe venire gravemente danneggiato. Prima di modificare il Registro di sistema, è consigliabile eseguire il backup di tutti i dati importanti disponibili nel computer. Se si riscontrano problemi dopo l'applicazione di modifiche manuali, è inoltre possibile utilizzare l'opzione di avvio Ultima configurazione valida nota.  
  
 Per altre informazioni sulle informazioni raccolte, elaborate o trasmesse dal programma Analisi utilizzo software, vedere l'[Informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=868444).  
 
### <a name="choice-and-control-over-ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Scelta e controllo per Analisi utilizzo software e SQL Server Data Tools per Visual Studio 2015  
 SSDT per Visual Studio 2015 è lo strumento di modellazione dei dati fornito con SQL Server 2016. Usa le opzioni di Analisi utilizzo software integrate in Visual Studio 2015. In questo [documento della Guida da Visual Studio](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017) sono disponibili altre informazioni sull'invio di commenti e suggerimenti con Analisi utilizzo software in Visual Studio 2015.  
  
 Nelle versioni di anteprima di SQL Server 2016, la funzionalità Analisi utilizzo software è attivata per impostazione predefinita. È possibile disattivarla o riattivarla seguendo le istruzioni seguenti.  
  
 **In Visual Studio (si applica alle installazioni complete di Visual Studio 2015)**  
  
 Se si esegue l'installazione di SSDT in un computer che dispone già di Visual Studio, vengono aggiunti solo i modelli di progetto Business Intelligence e SQL Server. In questo scenario, le opzioni per l'invio di commenti e suggerimenti offerte da Visual Studio possono essere usare per il consenso o il rifiuto esplicito per Analisi utilizzo software.  
  
1.  Avviare Visual Studio.  
  
2.  Dal menu Guida, selezionare **Invia commenti e suggerimenti** > **Impostazioni**.  
  
3.  Per disattivare Analisi utilizzo software, fare clic su **No, non desidero partecipare**, quindi fare clic su **OK**.  
  
     Per attivare Analisi utilizzo software, fare clic su **Sì, desidero partecipare al programma**, quindi fare clic su **OK**.  
  

  
 **Usare criteri basati sul Registro di sistema o Criteri di gruppo**  
  
 Se si esegue l'installazione di SSDT in un computer che non dispone di Visual Studio 2015, verrà installato solo Visual Studio Shell. La shell non fornisce opzioni per i suggerimenti dei clienti. In questo caso, un aggiornamento del Registro di sistema è l'unica opzione per la configurazione di Analisi utilizzo software.  
  
 I clienti aziendali possono creare Criteri di gruppo per partecipare o meno, impostando criteri basati sul Registro di sistema per SQL Server 2016.  
  
 Le relative impostazioni e chiavi del Registro di sistema sono le seguenti:  
  
 Chiave = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 Nome RegEntry = OptIn  
  
 Tipo voce DWORD:  
  
-   0 è rifiutare esplicitamente  
  
-   1 è acconsentire esplicitamente  
  
> [!CAUTION]  
>  Se il Registro di sistema viene modificato in modo non appropriato, il sistema potrebbe venire gravemente danneggiato. Prima di modificare il Registro di sistema, è consigliabile eseguire il backup di tutti i dati importanti disponibili nel computer. Se si riscontrano problemi dopo l'applicazione di modifiche manuali, è inoltre possibile utilizzare l'opzione di avvio Ultima configurazione valida nota.  
  
 Per altre informazioni sulle informazioni raccolte, elaborate o trasmesse dal programma Analisi utilizzo software, vedere l'[Informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=868444).  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>Scelta e controllo per il programma Analisi utilizzo software e SQL Server Data Tools - BI (SSDT-BI)  
 Se si usa SSDT-BI, l'utente potrà scegliere di partecipare ad Analisi utilizzo software durante l'installazione. In seguito, le modifiche alla configurazione di Analisi utilizzo software per SSDT-BI possono essere apportate mediante gli strumenti client o modificando le impostazioni del Registro di sistema.  
  
 **In SSDT e SSDT-BI per Visual studio 2013**  
  
1.  Avviare lo strumento e aprire un progetto nuovo o esistente di Analysis Services o Integration Services.  
  
2.  Scegliere **Opzioni commenti e suggerimenti utenti di Microsoft SQL Server**dal menu ?.  
  
3.  Per disattivare Analisi utilizzo software, fare clic su **No, non desidero partecipare**.  
  
     Per attivare Analisi utilizzo software, fare clic su **Sì, desidero partecipare**.  
  
4.  Fare clic su **OK**.  
  
 **Usare criteri basati sul Registro di sistema o Criteri di gruppo**  
  
 I clienti aziendali possono creare Criteri di gruppo per partecipare o meno impostando criteri basati sul Registro di sistema per SQL Server 2014.  
  
 Le relative impostazioni e chiavi del Registro di sistema sono le seguenti:  
  
 Chiave = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 Nome RegEntry = CustomerFeedback  
  
 Tipo voce DWORD:  
  
-   0 è rifiutare esplicitamente  
  
-   1 è acconsentire esplicitamente  
  
  
