---
title: Configurare DQS per l'uso di dati di riferimento | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.rdsconfiguration.f1
- sql13.dqs.administration.configuration.createDirectRDS.f1
- sql13.dqs.admin.config.rds.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd0987cfe98f8cb72531bf807494af1867646dcf
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617235"
---
# <a name="configure-dqs-to-use-reference-data"></a>Configurazione di DQS per l'utilizzo di dati di riferimento

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritta la procedura di configurazione di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) per l'utilizzo di dati di riferimento nelle attività di pulizia dei dati. È possibile utilizzare dati di riferimento da Windows Azure Marketplace o direttamente dai provider di dati di riferimento di terze parti online.  

> [!IMPORTANT]
> Questo articolo cita servizi dati di riferimento di terze parti che in precedenza erano disponibili in Azure DataMarket. DataMarket e i Servizi dati, inclusi ad esempio i dati di indirizzi Melissa, non sono più disponibili a partire dal 31/12/2016. Di conseguenza non è più possibile eseguire gli esempi di questo articolo con i servizi specificati di DataMarket. È comunque possibile usare servizi di dati di riferimento, disponibili direttamente online da provider di dati di riferimento terzi.

## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per utilizzare dati di riferimento da Marketplace, è necessario disporre di una chiave account Marketplace valida. Per informazioni dettagliate sulla creazione di una chiave account Marketplace, vedere [Creazione di un account](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936). La chiave account Marketplace può inoltre essere creata dall'interno di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] facendo clic su **Configurazione** in **Amministrazione** nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] e scegliendo **Crea ID account DataMarket** nella scheda **Dati di riferimento** .  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per configurare le impostazioni per il servizio dati di riferimento in DQS, è necessario disporre del ruolo dqs_administrator per il database DQS_MAIN.  
  
##  <a name="Marketplace"></a> Configurazione di DQS per l'utilizzo di dati di riferimento da Marketplace  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , in **Amministrazione**, fare clic su **Configurazione**.  
  
3.  Nella scheda **Dati di riferimento** , nell'area **Impostazioni di rete** digitare i valori appropriati nelle caselle **Server proxy** e **Porta** se l'organizzazione utilizza un server proxy per connettersi a Internet.  
  
4.  Specificare la chiave account Marketplace nella casella **ID account DataMarket** e fare clic sull'icona **Convalida ID account DataMarket** per convalidare la chiave account. Viene visualizzato un messaggio che informa se la chiave account Marketplace specificata è valida.  
  
 È ora possibile utilizzare in DQS i servizi dati di riferimento Marketplace sottoscritti per la chiave account Marketplace specificata.  
  
##  <a name="ThirdParty"></a> Configurazione di DQS per l'utilizzo di dati di riferimento direttamente da provider di dati di riferimento di terze parti online  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , in **Amministrazione**, fare clic su **Configurazione**.  
  
3.  Nella scheda **Dati di riferimento** , nell'area **Impostazioni di rete** digitare i valori appropriati nelle caselle **Server proxy** e **Porta** se l'organizzazione utilizza un server proxy per connettersi a Internet.  
  
4.  Nell'area **Impostazioni del servizio dati di riferimento di terze parti online diretto** , fare clic sull'icona **Aggiungi nuovo provider del servizio dati di riferimento** .  
  
5.  Nella finestra di dialogo **Crea nuovo provider del servizio dati di riferimento di terze parti online diretto** specificare i dettagli seguenti:  
  
    1.  Nella finestra di dialogo **Nome** digitare un nome per il nuovo provider del servizio dati di riferimento diretto.  
  
    2.  (Nella finestra di dialogo **Descrizione** digitare una descrizione per il nuovo provider del servizio dati di riferimento diretto (opzione facoltativa).  
  
    3.  Nella finestra di dialogo **Categoria** digitare la categoria dei dati forniti dal nuovo provider del servizio dati di riferimento diretto.  
  
    4.  Nella casella Schema, specificare lo schema che definisce la sequenza di campi (nomi colonna) da utilizzare dal provider del servizio dati di riferimento diretto. Un nome campo non deve contenere spazi e i campi devono essere separati da virgole. Esempio: `FirstName, LastName, City, State`.  
  
    5.  Nella finestra di dialogo **URI** digitare l'URI del nuovo provider del servizio dati di riferimento diretto. In DQS sono consentiti unicamente URI sicuri (con indirizzo che inizia per "https://").  
  
    6.  Nella casella **Dimensioni massime batch** , digitare il numero massimo di record per batch che verrà inviato al provider del servizio dati di riferimento per la pulizia. È possibile specificare un massimo di 100 record per batch per l'attività di pulizia.  
  
    7.  Nella finestra di dialogo **ID account** digitare l'ID account del sottoscrittore al provider del servizio dati di riferimento.  
  
6.  Scegliere **OK** per salvare i dati e chiudere la finestra di dialogo **Crea nuovo provider del servizio dati di riferimento di terze parti online diretto** . Il provider di dati di riferimento di terze parti online diretto appena aggiunto diventa disponibile nella **Griglia provider del servizio dati di riferimento diretti** in DQS.  
  
 È ora possibile utilizzare i servizi dati di riferimento dal provider del servizio dati di riferimento di terze parti online diretto appena aggiunto in DQS.  
  
##  <a name="FollowUp"></a> Completamento: Dopo avere Configurato DQS per l'utilizzo dei dati di riferimento  
 È ora necessario eseguire il mapping dei domini della Knowledge Base richiesti ai dati di riferimento disponibili dai provider di dati appena configurati. Per eseguire tale operazione, vedere [Collegare un dominio o un dominio composito ai dati di riferimento](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
  
