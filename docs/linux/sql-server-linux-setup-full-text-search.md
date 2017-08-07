---
title: Installazione di ricerca Full-Text SQL Server in Linux | Documenti Microsoft
description: In questo argomento viene descritto come installare ricerca Full-Text di SQL Server in Linux.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 8dd5d857efc47a0dc181a0fc9bf1537cb8b08441
ms.contentlocale: it-it
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-full-text-search-on-linux"></a>Installazione di ricerca Full-Text SQL Server in Linux

Installare i seguenti passaggi [ricerca Full-Text di SQL Server](https://msdn.microsoft.com/library/ms142571.aspx) (**mssql-server-fts**) in Linux. Ricerca full-Text consente di eseguire query full-text su dati di tipo carattere nelle tabelle di SQL Server. Per i problemi noti per questa versione, vedere il [note sulla versione](sql-server-linux-release-notes.md).

> [!NOTE]
> Prima di installare prima di ricerca Full-Text di SQL Server, [installare SQL Server](sql-server-linux-setup.md#platforms). Ciò consente di configurare le chiavi e i repository che durante l'installazione di **mssql-server-fts** pacchetto.

Installare ricerca Full-Text di SQL Server per la piattaforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Installare su RHEL</a>

Utilizzare i comandi seguenti per installare il **mssql-server-fts** su Red Hat Enterprise Linux. 

```bash
sudo yum update
sudo yum install -y mssql-server-fts
```

Se si dispone già di **mssql-server-fts** installato, è possibile aggiornare la versione più recente con i comandi seguenti:

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

Se occorre un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Quindi utilizzare gli stessi passaggi di installazione offline descritti nell'argomento [installazione di SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Installare in Ubuntu</a>

Utilizzare i comandi seguenti per installare il **mssql-server-fts** in Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

Se si dispone già di **mssql-server-fts** installato, è possibile aggiornare la versione più recente con i comandi seguenti:

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

Se occorre un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Quindi utilizzare gli stessi passaggi di installazione offline descritti nell'argomento [installazione di SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Installare in SLES</a>

Utilizzare i comandi seguenti per installare il **mssql-server-fts** in SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-fts
```

Se si dispone già di **mssql-server-fts** installato, è possibile aggiornare la versione più recente con i comandi seguenti:

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

Se occorre un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Quindi utilizzare gli stessi passaggi di installazione offline descritti nell'argomento [installazione di SQL Server](sql-server-linux-setup.md#offline).

## <a name="supported-languages"></a>Lingue supportate

Ricerca full-Text utilizza [word breaker](https://msdn.microsoft.com/library/ms142509.aspx) che determinano come identificare singole parole basate sul linguaggio. È possibile ottenere un elenco di word breaker registrati eseguendo una query di **Sys. fulltext_languages** vista del catalogo. Con SQL Server 2017 RC2 vengono installati i Word breaker per le lingue seguenti:

| Lingua | ID di lingua |
|---|---|
| Lingua neutra | 0 |
| Arabo | 1025 |
| Bengali (India) | 1093 |
| Bokmål | 1044 |
| Portoghese (Brasile) | 1046 |
| Inglese (Regno Unito) | 2057 |
| Bulgaro | 1026 |
| Catalano | 1027 |
| Cinese (Hong Kong - R.A.S., Repubblica popolare cinese) | 3076 |
| Cinese (Macao - R.A.S.) | 5124 |
| Cinese (Singapore) | 4100 |
| Croato | 1050 |
| Ceco | 1029 |
| Danese | 1030 |
| Olandese | 1043 |
| Inglese | 1033 |
| Francese | 1036 |
| Tedesco | 1031 |
| Greco | 1032 |
| Gujarati | 1095 |
| Hebrew | 1037 |
| Hindi | 1081 |
| Islandese | 1039 |
| Indonesiano | 1057 |
| Italiano | 1040 |
| Giapponese | 1041 |
| Kannada | 1099 |
| Coreano | 1042 |
| Lettone | 1062 |
| Lituano | 1063 |
| Malese (Malesia) | 1086 |
| Malayalam | 1100 |
| Marathi | 1102 |
| Polacco | 1045 |
| Portoghese | 2070 |
| Punjabi | 1094 |
| Romeno | 1048 |
| Russo | 1049 |
| Serbo (alfabeto cirillico) | 3098 |
| Serbo (alfabeto latino) | 2074 |
| Cinese semplificato | 2052 |
| Slovacco | 1051 |
| Sloveno | 1060 |
| Spagnolo | 3082 |
| Svedese | 1053 |
| Tamil | 1097 |
| Telugu | 1098 |
| Thai | 1054 |
| Cinese tradizionale | 1028 |
| Turco | 1055 |
| Ucraino | 1058 |
| Urdu | 1056 |
| Vietnamita | 1066 |

## <a id="filters"></a>Filtri

Ricerca full-Text funziona anche con il testo archiviato in file binari. Ma in questo caso, un filtro installato è necessario elaborare il file. Per ulteriori informazioni sui filtri, vedere [configurare e gestire i filtri per la ricerca](https://msdn.microsoft.com/library/ms142499.aspx).

È possibile visualizzare un elenco di filtri installati chiamando **sp_help_fulltext_system_components 'filter'**. Per SQL Server 2017 RC2, vengono installati i seguenti filtri:

| Nome componente | ID classe | Version |
|---|---|---|
|con estensione | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ANS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ASC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|ASM | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ASP | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|con estensione aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|ASX | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|BAS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|file con estensione bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CLS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.CSA | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CSS | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|CSV | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.DBS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|DOS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. DSP | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.FAQ | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.HHC | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|HTA | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|HTML | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|HTX | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ICS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|IDL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|IDQ | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|INF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|INI | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|INX | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|JAV | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|MAK | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.MK | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Con estensione odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ODL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|PL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.PRC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|RC | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RC2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|RCT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RGS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. RTF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|SCC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|sHTML | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.SOL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|SRF | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|STM | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|TAB | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TDL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TRG | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|UDF | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.UDT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|URL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|file con estensione vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|e vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>Ricerca semantica
[Ricerca semantica](https://msdn.microsoft.com/library/gg492075.aspx) si basa sulla funzionalità di ricerca Full-Text per estrarre e indice statisticamente pertinenti *frasi chiave*. Ciò consente di eseguire una query il significato all'interno di documenti nel database. Consente inoltre di identificare documenti simili.

Per utilizzare la ricerca semantica, è innanzitutto necessario scaricare e collegare il [database di statistiche lingua semantica](https://msdn.microsoft.com/library/gg509085.aspx).

1. In un computer Windows, [scaricare la. File con estensione MSI per il database di statistiche lingua semantica](https://www.microsoft.com/download/details.aspx?id=54277).

    > [!NOTE]
    > In questa fase il download per il database è una. File MSI, in modo da un computer Windows è necessario per questo passaggio.

2. Eseguire il. File MSI per estrarre il database e i file di log.

3. Spostare i file di database e del log nel computer Linux SQL Server.

    > [!TIP]
    > Per istruzioni su come spostare i file da Windows per Linux, vedere [trasferire un file in Linux](sql-server-linux-migrate-restore-database.md#transfer-the-backup-file-to-linux).

4. Eseguire il comando Transact-SQL seguente sull'istanza per collegare il database di statistiche lingua Linux SQL Server.

    ```tsql
    CREATE DATABASE semanticsdb  
            ON ( FILENAME = N'var/opt/mssql/data/semanticsdb.mdf' )  
            LOG ON ( FILENAME = N'var/opt/mssql/data/semanticsdb_log.ldf' )  
            FOR ATTACH;  
    GO  
    ```

5. Eseguire il comando Transact-SQL seguente per registrare il database di statistiche lingua semantica.

    ```tsql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO  
    ```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla ricerca Full-Text, vedere [ricerca Full-Text di SQL Server](../relational-databases/search/full-text-search.md). 
