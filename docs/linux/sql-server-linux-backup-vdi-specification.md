---
title: Specifica del Backup VDI - SQL Server in Linux
description: SQL Server Backup Virtual Device Interface Specification.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: 7c684170ae6ca6420b6b5ebef91baae208ab0808
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834196"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server nel client Linux VDI SDK specifica

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo documento descrive le interfacce fornite da SQL Server per il SDK del client Linux virtual device interface (VDI). Fornitori di software indipendenti (ISV) possono usare la Virtual Backup Device interfaccia API (Application Programming) per integrare SQL Server nei loro prodotti. In generale, VDI in Linux si comporta in modo analogo a un'infrastruttura VDI in Windows con le modifiche seguenti:

- Memoria condivisa di Windows diventa memoria POSIX condiviso.
- I semafori Windows diventano i semafori POSIX.
- Tipi di Windows, ad esempio HRESULT e DWORD vengono modificati agli equivalenti di integer.
- Le interfacce COM vengono rimosse e sostituite con una coppia di classi C++.
- SQL Server in Linux non supporta le istanze denominate in modo che i riferimenti al nome dell'istanza sono stati rimossi. 
- Libreria condivisa viene implementata in libsqlvdi.so installato presso /opt/mssql/lib/libsqlvdi.so

Questo documento è un addendum alle **vbackup.chm** che illustra in dettaglio la specifica di un'infrastruttura VDI di Windows. Scaricare il [Windows VDI specifica](https://www.microsoft.com/download/details.aspx?id=17282).

Esaminare anche la soluzione backup VDI di esempio nella [repository GitHub degli esempi di SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Impostazione delle autorizzazioni utente

In Linux, le primitive POSIX sono proprietà dell'utente la creazione di essi e al gruppo predefinito. Per gli oggetti creati da SQL Server, questi saranno per impostazione predefinita di proprietà di utente mssql e il gruppo mssql. Per consentire la condivisione tra SQL Server e client VDI, uno dei due metodi seguenti sono consigliati:

1. Eseguire il Client VDI come l'utente mssql
   
   Eseguire il comando seguente per passare all'utente mssql:
   
   ```bash
   sudo su mssql
   ```

2. Aggiungere l'utente mssql al gruppo del vdiuser e il vdiuser al gruppo mssql.
   
   Eseguire i comandi seguenti:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Riavviare il server di rilevare i nuovi gruppi per SQL Server e vdiuser

## <a name="client-functions"></a>Funzioni client

In questo capitolo contiene le descrizioni di tutte le funzioni client. Le descrizioni di includono le informazioni seguenti:

- Scopo della funzione
- Sintassi della funzione
- elenco di parametri
- Valori restituiti
- Note

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**Scopo** questa funzione crea il set di dispositivi virtuali.

**Sintassi**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| | **name** | Identifica il set di dispositivi virtuali. Le regole per i nomi utilizzati dai CreateFileMapping() devono essere seguite. Qualsiasi carattere eccetto barra rovesciata (\) può essere utilizzato. Si tratta di una stringa di caratteri. È consigliabile facendolo precedere la stringa con nome di prodotto o della società dell'utente e nome del database. |
| |**cfg** | Questa è la configurazione per il set di dispositivo virtuale. Per altre informazioni, vedere "Configurazione" più avanti in questo documento.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** | Funzione completata. |
| |**VD_E_NOTSUPPORTED** |Uno o più dei campi nella configurazione non è valido o in caso contrario, non è supportato. |
| |**VD_E_PROTOCOL** | Il dispositivo virtuale impostato già esistente.

**La sezione Osservazioni** creare il metodo deve essere chiamato solo una volta per ogni operazione di BACKUP o ripristino. Dopo aver richiamato il metodo Close, il client può riutilizzare l'interfaccia per creare un altro set di dispositivo virtuale.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Scopo** questa funzione viene utilizzata per attendere che il server configurare il set di dispositivi virtuali.
**Sintassi**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| | **timeout** | Si tratta del timeout in millisecondi. Consente di impedire i timeout infinito o qualsiasi numero intero negativo.
| | **cfg** | Al termine dell'esecuzione, contiene la configurazione selezionata dal server. Per altre informazioni, vedere "Configurazione" più avanti in questo documento.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** | La configurazione è stata restituita.
| |**VD_E_ABORT** |È stato richiamato SignalAbort.
| |**VD_E_TIMEOUT** |La funzione verifica il timeout.

**La sezione Osservazioni** questa funzione blocca in uno stato di avviso. Dopo una chiamata ha esito positivo, i dispositivi nel set di dispositivo virtuale possono essere aperta.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Scopo** questa funzione consente di aprire uno dei dispositivi nel set di dispositivo virtuale.
**Sintassi**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| | **name** |Identifica il set di dispositivi virtuali.
| | **ppVirtualDevice** |Quando la funzione ha esito positivo, viene restituito un puntatore al dispositivo virtuale. Questo dispositivo viene usato per l'operazione GetCommand e CompleteCommand.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Funzione completata.
| |**VD_E_ABORT** | È stato richiesto Abort.
| |**VD_E_OPEN** |  Tutti i dispositivi sono aperti.
| |**VD_E_PROTOCOL** |  Il set non è nello stato di inizializzazione o il dispositivo è già aperto.
| |**VD_E_INVALID** |Il nome del dispositivo non è valido. Non è uno dei nomi noti dovranno includere il set.

**La sezione Osservazioni** VD_E_OPEN può essere restituito senza problemi. Il client può chiamare OpenDevice mezzo di un ciclo fino a quando non viene restituito il codice.
Se è configurato più di un dispositivo, ad esempio *n* i dispositivi, verrà restituito il set di dispositivi virtuali *n* interfacce univoco del dispositivo.

Il `GetConfiguration` funzione può essere usata per attendere fino a quando i dispositivi possono essere aperti.
Se questa funzione non riesce, viene restituito un valore null tramite il ppVirtualDevice.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Scopo** questa funzione viene utilizzata per ottenere il successivo comando in coda in un dispositivo. Quando richiesto, questa funzione è in attesa per il comando successivo.

**Sintassi**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**timeout** |Questo è il tempo di attesa, espresso in millisecondi. Usare finito per un'attesa indefinita. Usare 0 per eseguire il polling di un comando. Se non è attualmente disponibile alcun comando, viene restituito VD_E_TIMEOUT. Se si verifica il timeout, il client decide l'azione successiva.
| |**Timeout** |Questo è il tempo di attesa, espresso in millisecondi. Usare finito o un valore negativo per un'attesa indefinita. Usare 0 per eseguire il polling di un comando. Se non è disponibile alcun comando prima che il timeout scade, viene restituito VD_E_TIMEOUT. Se si verifica il timeout, il client decide l'azione successiva.
| |**ppCmd** |Quando un comando viene restituito correttamente, il parametro restituisce l'indirizzo di un comando da eseguire. La memoria restituita è di sola lettura. Quando il comando viene completato, questo puntatore viene passato alla routine CompleteCommand. Per informazioni dettagliate su ogni comando, vedere la sezione "Commands" più avanti in questo documento.
        
| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |È stato recuperato un comando.
| |**VD_E_CLOSE** |Il dispositivo è stato chiuso dal server.
| |**VD_E_TIMEOUT** |Nessun comando è disponibile e il timeout è scaduto.
| |**VD_E_ABORT** |Client o il server ha usato la SignalAbort per forzare l'arresto.

**La sezione Osservazioni** VD_E_CLOSE quando viene restituito, SQL Server ha chiuso il dispositivo. Questo fa parte dell'arresto normale. Dopo che tutti i dispositivi sono stati chiusi, il client richiama ClientVirtualDeviceSet::Close per chiudere il set di dispositivi virtuali.
Quando questa routine deve bloccarsi in attesa per un comando, il thread è disponibile in una condizione di avviso.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Scopo** questa funzione viene utilizzata per notificare a SQL Server che ha completato un comando. Informazioni sul completamento appropriati per il comando deve essere restituiti. Per altre informazioni, vedere la sezione "Commands" più avanti in questo documento.

**Sintassi** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**pCmd** |Questo è l'indirizzo di un comando restituito precedentemente dal ClientVirtualDevice::GetCommand.
| |**completionCode** |Si tratta di un codice di stato che indica lo stato di completamento. Questo parametro deve essere restituito per tutti i comandi. Il codice restituito deve essere appropriato per il comando in esecuzione. ERROR_SUCCESS viene usato in tutti i casi per indicare un comando eseguito correttamente. Per l'elenco completo dei possibili codici, vedere il file, vdierror.h. Viene visualizzato un elenco dei codici di stato tipici per ogni comando in "Commands" più avanti in questo documento.
| |**bytesTransferred** |Questo è il numero di byte trasferiti. Viene restituito solo per il trasferimento di dati, i comandi di lettura e scrittura.
| |**position** |Si tratta di una risposta al comando GetPosition solo.
        
| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Il completamento corretto è stato osservato.
| |**VD_E_INVALID** |pCmd non era un comando attivo.
| |**VD_E_ABORT** |Abort è stata segnalata.
| |**VD_E_PROTOCOL** |Il dispositivo non è aperto.

**La sezione Osservazioni** None

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Scopo** questa funzione viene utilizzata per segnalare che non deve verificarsi un arresto anomalo.

**Sintassi** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |Nessuna | Non applicabile
        
| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR**|La notifica di interruzione è stata registrata correttamente.

**La sezione Osservazioni** in qualsiasi momento, il client può scegliere di interrompere l'operazione di BACKUP o ripristino. Questa routine segnala che devono interrompere tutte le operazioni. Lo stato del set di dispositivo virtuale complessiva entra in uno stato terminato in modo anomalo. Viene restituito alcun comando ulteriormente in qualsiasi dispositivo. Tutti i comandi incompiuti vengono completati automaticamente, restituendo 995L come un codice di completamento. Il client deve chiamare ClientVirtualDeviceSet::Close dopo che è terminato in modo sicuro qualsiasi utilizzo dei buffer fornito al client in sospeso. Per altre informazioni, vedere "Terminazione anomala" più indietro in questo documento.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Scopo** questa funzione consente di chiudere il set di dispositivi virtuali creato da ClientVirtualDeviceSet::Create. Restituisce la versione di tutte le risorse associate al set di dispositivo virtuale.

**Sintassi** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |Nessuna |Non applicabile
        
| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Viene restituito quando il set di dispositivo virtuale è stata chiusa correttamente.
| |**VD_E_PROTOCOL** |È stata eseguita alcuna azione perché il set di dispositivo virtuale non era aperto.
| |**VD_E_OPEN** |I dispositivi sono stati ancora aperti.

**La sezione Osservazioni** la chiamata di Close è una dichiarazione di client che devono essere rilasciate tutte le risorse usate dal set di dispositivo virtuale. Il client deve verificare che tutte le attività che coinvolgono i buffer dei dati e i dispositivi virtuali sono terminata prima di richiamare una chiusura. Tutte le interfacce di dispositivo virtuale restituite dalla OpenDevice vengono invalidate da chiudere.
Il client è consentito dopo la chiamata di chiusura viene restituito a una chiamata di creazione dell'interfaccia di set di dispositivo virtuale. Tale chiamata crea un nuovo dispositivo virtuale impostato per un'operazione di BACKUP o RESTORE successiva.
Se Chiudi viene chiamato quando uno o più dispositivi virtuali vengono ancora aperti, viene restituito VD_E_OPEN. In questo caso, SignalAbort viene attivata internamente, per garantire una corretta chiusura se possibile. Vengono rilasciate le risorse di infrastruttura VDI. Il client deve attendere per un'indicazione VD_E_CLOSE su ogni dispositivo prima di richiamare ClientVirtualDeviceSet::Close. Se il client sa che il set di dispositivo virtuale è già in uno stato terminato in modo anomalo, quindi non possono prevedere un'indicazione VD_E_CLOSE dall'operazione GetCommand e può richiamare ClientVirtualDeviceSet::Close appena attività su buffer condiviso viene terminato.
Per altre informazioni, vedere "Terminazione anomala" più indietro in questo documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Scopo** questa funzione consente di aprire il dispositivo virtuale impostato in un client secondario. Il client primario deve avere già usato GetConfiguration e crea per configurare il set di dispositivi virtuali.

**Sintassi** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**setName** |Identifica il set. Questo nome è distinzione maiuscole/minuscole e deve corrispondere al nome usato dal client primario, quando richiamata ClientVirtualDeviceSet::Create.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Funzione completata.
| |**VD_E_PROTOCOL** |Il set di dispositivi virtuali non è stato creato, è già stata aperta in questo client o il dispositivo virtuale set non è pronto ad accettare richieste aperte dai client secondario.
| |**VD_E_ABORT** |L'operazione è in corso interrotta.

**La sezione Osservazioni** quando si usa un modello di processo più, il client primario è responsabile del rilevamento normale e anomala terminazione dei client secondario.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Scopo** alcune applicazioni possono richiedere più di un processo su cui operare i buffer restituiti da ClientVirtualDevice::GetCommand. In questi casi, il processo che riceve il comando è possibile usare GetBufferHandle per ottenere un handle di processo indipendenti che identifica il buffer. Questo handle può quindi essere comunicato a qualsiasi altro processo che ha anche l'apertura di Set di dispositivi virtuali stesso. Tale processo sarebbe quindi usare ClientVirtualDeviceSet::MapBufferHandle per ottenere l'indirizzo del buffer. L'indirizzo sarà probabilmente un indirizzo diverso da quello nel relativo partner poiché ogni processo può eseguire il mapping di buffer in indirizzi diversi.

**Sintassi** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**pBuffer** |Questo è l'indirizzo di un buffer ottenuto da un comando di lettura o scrittura.
| |**BufferHandle** |Viene restituito un identificatore univoco per il buffer.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Funzione completata.
| |**VD_E_PROTOCOL** |Il set di dispositivo virtuale non è attualmente aperto.
| |**VD_E_INVALID** |Il pBuffer non è un indirizzo valido.

La sezione Osservazioni il processo che richiama la funzione GetBufferHandle è responsabile del richiamo ClientVirtualDevice::CompleteCommand durante il trasferimento dei dati è stato completato.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Scopo** questa funzione viene utilizzata per ottenere un indirizzo di buffer valida da un handle del buffer ottenuto da un altro processo. 

**Sintassi** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parametri | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**dwBuffer** |Questo è l'handle restituito da ClientVirtualDeviceSet::GetBufferHandle.
| |**ppBuffer** |Questo è l'indirizzo dei buffer valido nel processo corrente.

| Valori restituiti | Argomento | Spiegazione
| ----- | ----- | ------ |
| |**NOERROR** |Funzione completata.
| |**VD_E_PROTOCOL** |Il set di dispositivo virtuale non è attualmente aperto.
| |**VD_E_INVALID** |Il ppBuffer è un handle non valido.

**La sezione Osservazioni** necessario prestare attenzione per comunicare correttamente i punti di controllo. Gli handle sono locali rispetto a un set unico dispositivo virtuale. I processi di partner la condivisione di un handle devono garantire tale buffer gli handle vengono usati solo all'interno dell'ambito del dispositivo virtuale impostato da cui è stato originariamente ottenuto il buffer.


