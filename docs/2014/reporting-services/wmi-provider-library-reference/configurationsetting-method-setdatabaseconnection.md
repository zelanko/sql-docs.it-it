---
title: Metodo SetDatabaseConnection (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 02c15c6336171bb324f610b42c97559bcfb0d44b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026622"
---
# <a name="setdatabaseconnection-method-wmi-msreportserverconfigurationsetting"></a>Metodo SetDatabaseConnection (MSReportServer_ConfigurationSetting WMI)
  Imposta la connessione al database del server di report su un database del server di report specifico.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Server*  
 Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usata per ospitare il database del server di report.  
  
 *DatabaseName*  
 Nome del database del server di report.  
  
 *CredentialsType*  
 Tipo di credenziali da utilizzare per la connessione. I valori possibili sono i seguenti.  
  
-   0: Windows  
  
-   1: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2: servizio Windows  
  
 *UserName*  
 Nome account utilizzato per la connessione al database del server di report.  
  
 *Password*  
 Password utilizzata per la connessione al database del server di report.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Quando il parametro *CredentialsType* è impostato su 0 (Windows), è necessario impostare i parametri *UserName* e *Password* . Il parametro *UserName* deve avere il formato "dominio\nomeutente" e il valore deve rappresentare un account di accesso di Windows valido.  
  
 Quando il parametro *CredentialsType* è impostato su 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), il valore passato nel parametro *UserName* deve essere conforme ai requisiti di un nome account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Quando il parametro *CredentialsType* è impostato su 2 (servizio Windows), il server di report usa la sicurezza integrata per la connessione al database del server di report e i parametri *UserName* e *Password* vengono ignorati. Il servizio Web ReportServer userà l'account [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] o l'account del pool di applicazioni e l'account del servizio Windows per accedere al database del server di report.  
  
 Quando viene chiamato, il metodo SetDatabaseConnection crittografa e archivia le credenziali e le informazioni di database nel file di configurazione per il server di report specificato.  
  
 Il metodo SetDatabaseConnection non verifica che il server di report sia in grado di connettersi al database del server di report tramite i dati specificati.  
  
 Quando viene impostata per la prima volta, la proprietà ConnectionPoolSize viene impostata in base ai seguenti processori: ConnectionPoolSize = #Processors * 75.  
  
 Il metodo SetDatabaseConnection non concede autorizzazioni agli account specificati. È necessario chiamare il metodo [GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md) per ogni account che richiede l'accesso al database del server di report ed eseguire lo script risultante.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
