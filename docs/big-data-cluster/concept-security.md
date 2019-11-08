---
title: Concetti relativi alla sicurezza
titleSuffix: SQL Server big data clusters
description: Questo articolo presenta alcuni concetti relativi alla sicurezza per i cluster Big Data di SQL Server. È inclusa la descrizione degli endpoint del cluster e dell'autenticazione del cluster.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35eb5e0a3236d8f016ed5ca99b769d628a4d81ed
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532365"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Concetti relativi alla sicurezza per i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo presenta i concetti principali relativi alla sicurezza nel cluster Big Data

I [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] forniscono autorizzazione e autenticazione coerenti. Un cluster Big Data può essere integrato con Active Directory tramite una distribuzione completamente automatizzata dell'integrazione di Active Directory in un dominio esistente. Dopo aver configurato un cluster Big Data con l'integrazione di Active Directory, è possibile sfruttare le identità e i gruppi di utenti esistenti per l'accesso unificato in tutti gli endpoint. Inoltre, dopo avere creato tabelle esterne in SQL Server, è possibile controllare l'accesso alle origini dati concedendo l'accesso alle tabelle esterne a utenti e gruppi di Active Directory, centralizzando in questo modo i criteri di accesso ai dati in un'unica posizione.

## <a name="authentication"></a>Autenticazione

Gli endpoint del cluster esterni supportano l'autenticazione di Active Directory. Questo significa che è possibile usare l'identità di Active Directory per l'autenticazione nel cluster Big Data.

### <a name="cluster-endpoints"></a>Endpoint del cluster

Esistono cinque punti di ingresso al cluster Big Data

* Istanza master: endpoint TDS per l'accesso all'istanza master di SQL Server nel cluster, tramite strumenti di database e applicazioni come SSMS o Azure Data Studio. Quando si usano HDFS o comandi di SQL Server da azdata, lo strumento si connette agli altri endpoint, a seconda dell'operazione.

* Gateway per l'accesso a file HDFS, Spark (Knox): endpoint basato su HTTPS. Questo endpoint viene usato per accedere a servizi come webHDFS e Spark.

* Endpoint del servizio di gestione del cluster (controller): servizio di gestione del cluster Big Data che espone API REST per la gestione del cluster. Lo strumento azdata richiede la connessione a questo endpoint.

* Proxy di gestione: per l'accesso ai dashboard Ricerca log e Metriche.

* Proxy dell'applicazione: endpoint per la gestione delle applicazioni distribuite all'interno del cluster Big Data.

![Endpoint del cluster](media/concept-security/cluster_endpoints.png)

Attualmente non è possibile aprire porte aggiuntive per accedere al cluster dall'esterno.

## <a name="authorization"></a>Autorizzazione

In tutto il cluster la sicurezza integrata tra diversi componenti permette di passare l'identità dell'utente originale durante l'invio di query da Spark e SQL Server, fino ad HDFS. Come indicato sopra, i diversi endpoint del cluster esterni supportano l'autenticazione di Active Directory.

Esistono due livelli di controllo delle autorizzazioni nel cluster per la gestione dell'accesso ai dati. L'autorizzazione nel contesto dei Big Data viene eseguita in SQL Server, usando le autorizzazioni di SQL Server tradizionali per gli oggetti, e in HDFS con elenchi di controllo (ACL), che associano le identità utente ad autorizzazioni specifiche.

Un cluster Big Data sicuro implica un supporto costante e coerente per gli scenari di autenticazione e autorizzazione, sia in SQL Server sia in HDFS/Spark. L'autenticazione è il processo di verifica dell'identità di un utente o di un servizio per garantire che corrisponda a quella dichiarata dall'utente o dal servizio stesso. Per autorizzazione si intende la concessione o la negazione dell'accesso a risorse specifiche in base all'identità dell'utente richiedente. Questo passaggio viene eseguito dopo l'identificazione di un utente tramite l'autenticazione.

Nel contesto dei Big Data l'autorizzazione viene in genere eseguita tramite gli elenchi di controllo di accesso (ACL), che associano le identità utente ad autorizzazioni specifiche. HDFS supporta l'autorizzazione limitando l'accesso alle API del servizio, ai file HDFS e all'esecuzione del processo.

## <a name="encryption-and-other-security-mechanisms"></a>Crittografia e altri meccanismi di sicurezza

La crittografia delle comunicazioni tra i client e gli endpoint esterni, nonché tra i componenti all'interno del cluster, è protetta con TLS/SSL tramite certificati.

Tutte le comunicazioni da SQL Server a SQL Server, ad esempio la comunicazione dell'istanza master di SQL Server con un pool di dati, vengono protette tramite account di accesso SQL.

## <a name="basic-administrator-login"></a>Account di accesso amministratore di base

È possibile scegliere di distribuire il cluster in modalità Active Directory o solo con l'account di accesso amministratore di base. L'uso del solo account di accesso amministratore di base non è una modalità di sicurezza supportata per la produzione e questo account è adatto principalmente alla valutazione del prodotto.

Anche se si sceglie la modalità Active Directory, per l'amministratore del cluster vengono comunque creati account di accesso di base. Questo approccio fornisce un'alternativa quando la connettività ad Active Directory non è disponibile.

A questo account di accesso di base vengono concesse le autorizzazioni di amministratore nel cluster in fase di distribuzione. Questo significa che l'utente sarà un amministratore di sistema nell'istanza master di SQL Server e un amministratore nel controller del cluster.
I componenti Hadoop non supportano l'autenticazione in modalità mista e di conseguenza non è possibile usare un account di accesso amministratore di base per l'autenticazione nel gateway (Knox).


Queste sono le credenziali di accesso che è necessario definire in fase di distribuzione.

Nome utente dell'amministratore del cluster:
 + `AZDATA_USERNAME=<username>`

Password dell'amministratore del cluster:  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> Si noti che in modalità non Active Directory è necessario usare il nome utente "root" in combinazione con la password precedente, per l'autenticazione nel gateway (Knox) per l'accesso a HDFS/Spark.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vedere le risorse seguenti:

- [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Architettura Microsoft dei [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
