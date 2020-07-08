---
title: Stored procedure (catalogo di Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba8d5f185968cc46809e03654f6fe4c0f8b4f6de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85673617"
---
# <a name="stored-procedures-integration-services-catalog"></a>Stored procedure (catalogo di Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  In questa sezione vengono descritte le stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] disponibili per l'amministrazione di progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] distribuiti in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Chiamare le stored procedure di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per aggiungere, rimuovere, modificare o eseguire oggetti archiviati nel catalogo **SSISDB**.  
  
 Il nome predefinito del catalogo è SSISDB. Tra gli oggetti archiviati nel catalogo sono inclusi progetti, pacchetti, parametri, ambienti e cronologia operativa.  
  
 È possibile utilizzare le viste del database e le stored procedure direttamente oppure scrivere codice personalizzato con cui chiamare l'API gestita. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e l'API gestita eseguono query sulle viste e chiamano le stored procedure descritte in questa sezione per eseguire molte delle rispettive attività.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 Aggiunge una scelta dei dati sull'output di un componente in un flusso di dati del pacchetto.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 Aggiunge una scelta dei dati a un percorso del flusso di dati specifico in un flusso di dati del pacchetto.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 Determina se lo schema del catalogo SSISDB e i file binari (assembly ISServerExec e SQLCLR) di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono compatibili.  
  
 [catalog.clear_object_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 Viene cancellato il valore di un parametro per un progetto o pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esistente archiviato nel server.  
  
 [catalog.configure_catalog &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 Viene configurato il catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] impostando una proprietà del catalogo su un valore specificato.  
  
 [catalog.create_environment &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 Viene creato un ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_reference &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 Viene creato un riferimento all'ambiente per un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_variable &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 Crea una variabile di ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 Crea un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 Comporta la sospensione di un pacchetto in esecuzione e la creazione di un file di dump.  
  
 [catalog.create_folder &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 Crea una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 Viene eliminato un ambiente da una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_reference &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 Viene eliminato un riferimento all'ambiente da un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_variable &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 Viene eliminata una variabile di ambiente da un ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_folder &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 Viene eliminata una cartella dal catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 Viene eliminato un progetto esistente da una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.deny_permission &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 Viene negata un'autorizzazione su un oggetto a protezione diretta nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.deploy_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 Viene distribuito un progetto in una cartella del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o viene aggiornato un progetto esistente distribuito precedentemente.  
  
 [catalog.get_parameter_values &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 Vengono risolti e recuperati i valori predefiniti del parametro da un progetto e dai pacchetti corrispondenti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.get_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 Vengono recuperate le proprietà di un progetto esistente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.grant_permission &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 Viene concessa un'autorizzazione su un oggetto a protezione diretta nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_environment &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 Viene spostato un ambiente da una cartella a un'altra all'interno del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_project &#40;&#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
 Viene spostato un progetto da una cartella a un'altra all'interno del catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 Rimuove un data tap da un output del componente in esecuzione.  
  
 [catalog.rename_environment &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 Viene rinominato un ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.rename_folder &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 Rinomina una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.restore_project &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 Viene ripristinata la versione precedente di un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.revoke_permission &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 Viene revocata un'autorizzazione su un oggetto a protezione diretta nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_property &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 Viene impostata la proprietà di un ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_reference_type &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 Vengono impostati il tipo di riferimento e il nome dell'ambiente associato a un riferimento all'ambiente esistente per un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_property &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 Viene impostata la proprietà di una variabile di ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_protection &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 Viene impostato il bit di importanza di una variabile di ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_value &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 Viene impostato il valore di una variabile di ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Imposta il valore di un parametro per un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 Imposta il valore di una proprietà per un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_folder_description &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 Imposta la descrizione di una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_object_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 Viene impostato il valore di un parametro nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Viene associato il valore a una variabile di ambiente o viene assegnato un valore letterale che sarà utilizzato per impostazione predefinita nel caso non venga assegnato nessun altro valore.  
  
 [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 Viene avviata un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 Esegue la manutenzione dello stato delle operazioni per il catalogo SSISDB.  
  
 [catalog.stop_operation &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 Arresta una convalida o un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.validate_package &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 Viene convalidato in modo asincrono un pacchetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.validate_project &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 Viene convalidato in modo asincrono un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
[catalog.add_execution_worker &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Aggiunge un servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker a un'istanza di esecuzione in Scale Out.

[catalog.enable_worker_agent &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Abilita uno Scale Out Worker per lo Scale Out Master che interagisce con questo catalogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

[catalog.disable_worker_agent &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Disabilita uno Scale Out Worker per lo Scale Out Master che interagisce con questo catalogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].


