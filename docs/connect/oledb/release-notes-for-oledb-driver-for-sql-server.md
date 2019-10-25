---
title: Note sulla versione (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 350856cc27bdec601e0db2998f9ff9953cdf6ec7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381727"
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

Ottobre 2019

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto dell'autenticazione di Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| Supporto per Active Directory Authentication Library incorporato (ADAL). | Un'installazione separata di ADAL non è più necessaria per l'uso di determinati metodi di autenticazione. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione della logica di eliminazione degli indici in [IIndexDefinition::D ropindex](https://go.microsoft.com/fwlink/?linkid=2106448). | Le versioni precedenti del driver OLE DB non possono eliminare un indice di chiave primaria se l'ID dello schema e l'ID utente del proprietario dell'indice non sono uguali. |
| &nbsp; | &nbsp; |

## <a name="1823"></a>18.2.3

Giugno 2019

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per gli aggiornamenti dei driver dal SQL Server supporto rimovibile. | Questo miglioramento consente l'aggiornamento dei driver direttamente dal SQL Server supporto rimovibile. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

Maggio 2019

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione dell'autenticazione non interattiva di Azure Active Directory nell'apartment a thread multipli (MTA). | OLE DB Driver 18.2.1 prova erroneamente a modificare il modello di concorrenza COM in un apartment che è stato inizializzato in precedenza con thread multipli (MTA). Di conseguenza, in un'applicazione che effettua più di una chiamata successiva a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) o a [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) prima di chiamare l'interfaccia [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), il driver non riesce a connettersi quando si usa una qualsiasi modalità di autenticazione di Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

Febbraio 2019

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la codifica server UTF-8. | [Supporto di UTF-8 in OLE DB Driver per SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Supporto dell'autenticazione di Azure Active Directory. | [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Luglio 2018

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `UseFMTONLY` e per la proprietà di inizializzazione `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br/><br/>Per ulteriori informazioni, vedere [utilizzo delle parole chiave della stringa di connessione con il Driver OLE DB per SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione della versione errata del file di formato BCP. | OLE DB Driver 18.0 imposta in modo errato la versione del file di formato BCP su 18.0, anziché su 11.0.<br/>OLE DB Driver 18.1 non è in grado di leggere file di formato generati da OLE DB Driver 18.0.<br/>Se è necessario usare con il nuovo driver file di formato generati con la versione precedente, è possibile modificare manualmente i file in modo da impostare la versione su 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `MultiSubnetFailover` e la proprietà di inizializzazione `SSPROP_INIT_MULTISUBNETFAILOVER`. | Per altre informazioni, vedere:<br/>&bull; &nbsp; [Supporto di OLE DB Driver per SQL Server per il ripristino di emergenza a disponibilità elevata](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Driver Microsoft OLE DB per SQL Server](oledb-driver-for-sql-server.md)
