---
title: Schema delle impostazioni dell'applicazione
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema application settings
- application settings, schema [Windows Forms]
- Windows Forms, application settings schema
- configuration schema [.NET Framework], application settings
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
caps.latest.revision: "3"
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 3581c8079132de5f1faad4a01e6b43c8e4833316
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="application-settings-schema"></a>Schema delle impostazioni dell'applicazione

Le impostazioni dell'applicazione consentono a un'applicazione Windows Forms o ASP.NET archiviare e recuperare le impostazioni con ambito di applicazione e con ambito di utente. In questo contesto, un *impostazione* è qualsiasi informazione che possono essere specifici dell'applicazione o specifici dell'utente corrente, qualsiasi elemento da una stringa di connessione di database per l'utente preferita dimensione predefinita della finestra.

Per impostazione predefinita, le impostazioni dell'applicazione in un'applicazione Windows Form usa il <xref:System.Configuration.LocalFileSettingsProvider> (classe), che utilizza il sistema di configurazione .NET per archiviare le impostazioni in un file di configurazione XML. Per ulteriori informazioni sui file utilizzati dalle impostazioni dell'applicazione, vedere [architettura Impostazioni applicazione](~/docs/framework/winforms/advanced/application-settings-architecture.md).

Le impostazioni dell'applicazione definisce gli elementi seguenti come parte dei file di configurazione viene utilizzato.

| Elemento                    | Descrizione                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------- |
| **\<applicationSettings >** | Contiene tutti  **\<impostazione >** tag specifici dell'applicazione.                         |
| **\<userSettings >**        | Contiene tutti  **\<impostazione >** tag specifici per l'utente corrente.                        |
| **\<impostazione >**             | Definisce un'impostazione. Figlio di  **\<applicationSettings >** o  **\<userSettings >**. |
| **\<value>**               | Definisce un valore dell'impostazione. Elemento figlio di  **\<impostazione >**.                                   |

## <a name="applicationsettings-element"></a>\<applicationSettings > elemento

Questo elemento contiene tutti  **\<impostazione >** tag specifici a un'istanza dell'applicazione in un computer client. Non definisce alcun attributo.

## <a name="usersettings-element"></a>\<userSettings > elemento

Questo elemento contiene tutti  **\<impostazione >** tag specifici per l'utente che sta attualmente utilizzando l'applicazione. Non definisce alcun attributo.

## <a name="setting-element"></a>\<impostazione > elemento

Questo elemento definisce un'impostazione. Include gli attributi seguenti.

| Attributo        | Descrizione |
| ---------------- | ----------- |
| **name**         | Obbligatorio. ID univoco dell'impostazione. Le impostazioni create tramite Visual Studio vengono salvate con il nome `ProjectName.Properties.Settings`. |
| **serializedAs** | Obbligatorio. Il formato da utilizzare per la serializzazione del valore di testo. I valori validi sono:<br><br>- `string`. Il valore viene serializzato come una stringa usando un <xref:System.ComponentModel.TypeConverter>.<br>- `xml`. Il valore viene serializzato utilizzando la serializzazione XML.<br>- `binary`. Il valore viene serializzato in formato binario con codifica testo mediante la serializzazione binaria.<br />- `custom`. Il provider di impostazioni ha informazioni inerenti a questa impostazione e serializza e deserializza il. |

## <a name="value-element"></a>\<valore > elemento

Questo elemento contiene il valore di un'impostazione.

## <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato un file di impostazioni dell'applicazione che definisce due impostazioni con ambito di applicazione e due impostazioni con ambito di utente:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
    </sectionGroup>
    <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />
    </sectionGroup>
  </configSections>
  <applicationSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="Cursor" serializeAs="String">
        <value>Default</value>
      </setting>
      <setting name="DoubleBuffering" serializeAs="String">
        <value>False</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </applicationSettings>
  <userSettings>
    <WindowsApplication1.Properties.Settings>
      <setting name="FormTitle" serializeAs="String">
        <value>Form1</value>
      </setting>
      <setting name="FormSize" serializeAs="String">
        <value>595, 536</value>
      </setting>
    </WindowsApplication1.Properties.Settings>
  </userSettings>
</configuration>
```

## <a name="see-also"></a>Vedere anche

[Cenni preliminari sulle impostazioni delle applicazioni](~/docs/framework/winforms/advanced/application-settings-overview.md)   
[Application Settings Architecture](~/docs/framework/winforms/advanced/application-settings-architecture.md)
