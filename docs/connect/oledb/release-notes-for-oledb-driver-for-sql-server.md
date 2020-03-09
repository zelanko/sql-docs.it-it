---
title: Note sulla versione (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 02/27/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 8c06b83241f377aa05d7e5c0e4cb0d83a424f15a
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866230"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Note sulla versione per il driver Microsoft OLE DB per SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Questa pagina elenca le nuove funzionalità aggiunte o modificate in ogni versione di Microsoft OLE DB Driver for SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1830"></a>18.3.0

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2117515)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2117517)  

Resa disponibile: Ottobre 2019

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto dell'autenticazione di Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| Includere Azure Active Directory Authentication Library (adal.dll) nel programma di installazione | Ora inclusa nell'installazione del driver di base, verranno così aggiornate le installazioni esistenti di Microsoft Active Directory Authentication Library per SQL Server, rimuovendo l'applicazione dall'elenco delle applicazioni installate in Windows. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione della logica di eliminazione degli indici in [IIndexDefinition::DropIndex](https://go.microsoft.com/fwlink/?linkid=2106448). | Le versioni precedenti del driver OLE DB non possono eliminare un indice di chiave primaria se l'ID schema e l'ID utente del proprietario dell'indice non sono uguali. |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>Versioni precedenti

Scaricare le versioni precedenti del driver OLE DB facendo clic sui collegamenti di download nelle sezioni seguenti:

## <a name="1823"></a>18.2.3

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2119554)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2119738)  

Resa disponibile: Giugno 2019

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per gli aggiornamenti del driver dai supporti rimovibili di SQL Server. | Questo miglioramento consente gli aggiornamenti dei driver direttamente dai supporti rimovibili di SQL Server. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2118512)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2118415)  

Resa disponibile: Maggio 2019

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione dell'autenticazione non interattiva di Azure Active Directory nell'apartment a thread multipli (MTA). | OLE DB Driver 18.2.1 prova erroneamente a modificare il modello di concorrenza COM in un apartment che è stato inizializzato in precedenza con thread multipli (MTA). Di conseguenza, in un'applicazione che effettua più di una chiamata successiva a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) o a [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) prima di chiamare l'interfaccia [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), il driver non riesce a connettersi quando si usa una qualsiasi modalità di autenticazione di Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2118511)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2118278)  

Resa disponibile: Febbraio 2019

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la codifica server UTF-8. | [Supporto di UTF-8 in OLE DB Driver per SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Supporto dell'autenticazione di Azure Active Directory. | [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2118506)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2118509)  

Resa disponibile: Luglio 2018

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `UseFMTONLY` e per la proprietà di inizializzazione `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br/><br/>Per altre informazioni, vedere: [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione della versione errata del file di formato BCP. | OLE DB Driver 18.0 imposta in modo errato la versione del file di formato BCP su 18.0, anziché su 11.0.<br/>OLE DB Driver 18.1 non è in grado di leggere file di formato generati da OLE DB Driver 18.0.<br/>Se è necessario usare con il nuovo driver file di formato generati con la versione precedente, è possibile modificare manualmente i file in modo da impostare la versione su 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x64](https://go.microsoft.com/fwlink/?linkid=2118504)  
![download](../../ssms/media/download-icon.png) [Scaricare il programma di installazione x86](https://go.microsoft.com/fwlink/?linkid=2118277)  

Resa disponibile: Marzo 2018

Se è necessario scaricare il programma di installazione in una lingua diversa da quella rilevata, è possibile usare questi collegamenti diretti.  
Per il driver x64: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
Per il driver x86: [Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `MultiSubnetFailover` e la proprietà di inizializzazione `SSPROP_INIT_MULTISUBNETFAILOVER`. | Per altre informazioni, vedere:<br/>&bull; &nbsp; [Supporto di OLE DB Driver per SQL Server per il ripristino di emergenza a disponibilità elevata](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Driver Microsoft OLE DB per SQL Server](oledb-driver-for-sql-server.md)
