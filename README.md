# 👻 Modulo di Sicurezza Ghost
**Strumento di Hardening di Sicurezza Windows e Azure basato su PowerShell**

> **Hardening di sicurezza proattivo per endpoint Windows e ambienti Azure.** Ghost fornisce funzioni di hardening basate su PowerShell che possono aiutare a ridurre i vettori di attacco comuni disabilitando servizi e protocolli non necessari.

## ⚠️ Importanti Disclaimer

**TESTING RICHIESTO**: Testare sempre Ghost in ambienti non di produzione prima. La disabilitazione dei servizi può influire sulle funzioni aziendali legittime.

**NESSUNA GARANZIA**: Mentre Ghost prende di mira i vettori di attacco comuni, nessuno strumento di sicurezza può prevenire tutti gli attacchi. Questo è un componente di una strategia di sicurezza completa.

**IMPATTO OPERATIVO**: Alcune funzioni possono influire sulla funzionalità del sistema. Rivedere attentamente ogni impostazione prima del deployment.

**VALUTAZIONE PROFESSIONALE**: Per ambienti di produzione, consultare professionisti della sicurezza per assicurarsi che le impostazioni si allineino alle esigenze della vostra organizzazione.

## 📊 Il Panorama della Sicurezza

I danni da ransomware hanno raggiunto **$57 miliardi nel 2025**, con ricerche che indicano che molti attacchi riusciti sfruttano servizi Windows di base e configurazioni errate. I vettori di attacco comuni includono:

- **Il 90% degli incidenti ransomware** coinvolge lo sfruttamento RDP
- **Le vulnerabilità SMBv1** hanno abilitato attacchi come WannaCry e NotPetya  
- **Le macro dei documenti** rimangono un metodo primario di consegna malware
- **Gli attacchi basati su USB** continuano a prendere di mira le reti air-gapped
- **L'abuso di PowerShell** è aumentato significativamente negli ultimi anni

## 🛡️ Funzioni di Sicurezza Ghost

Ghost fornisce **16 funzioni di hardening Windows** più **integrazione di sicurezza Azure**:

### Hardening Endpoint Windows

| Funzione | Scopo | Considerazioni |
|----------|---------|----------------|
| `Set-RDP` | Gestisce l'accesso Remote Desktop | Può influire sull'amministrazione remota |
| `Set-SMBv1` | Controlla il protocollo SMB legacy | Richiesto per sistemi molto vecchi |
| `Set-AutoRun` | Controlla AutoPlay/AutoRun | Può influire sulla comodità dell'utente |
| `Set-USBStorage` | Limita i dispositivi di archiviazione USB | Può influire sull'uso legittimo USB |
| `Set-Macros` | Controlla l'esecuzione macro Office | Può influire sui documenti abilitati alle macro |
| `Set-PSRemoting` | Gestisce PowerShell remoting | Può influire sulla gestione remota |
| `Set-WinRM` | Controlla Windows Remote Management | Può influire sull'amministrazione remota |
| `Set-LLMNR` | Gestisce il protocollo di risoluzione nomi | Solitamente sicuro da disabilitare |
| `Set-NetBIOS` | Controlla NetBIOS su TCP/IP | Può influire sulle applicazioni legacy |
| `Set-AdminShares` | Gestisce le condivisioni amministrative | Può influire sull'accesso ai file remoti |
| `Set-Telemetry` | Controlla la raccolta dati | Può influire sulle capacità diagnostiche |
| `Set-GuestAccount` | Gestisce l'account Guest | Solitamente sicuro da disabilitare |
| `Set-ICMP` | Controlla le risposte ping | Può influire sulla diagnostica di rete |
| `Set-RemoteAssistance` | Gestisce Remote Assistance | Può influire sulle operazioni help desk |
| `Set-NetworkDiscovery` | Controlla la scoperta di rete | Può influire sulla navigazione di rete |
| `Set-Firewall` | Gestisce Windows Firewall | Critico per la sicurezza di rete |

### Sicurezza Cloud Azure

| Funzione | Scopo | Requisiti |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Abilita la sicurezza di base Azure AD | Permessi Microsoft Graph |
| `Set-AzureConditionalAccess` | Configura le policy di accesso | Licenze Azure AD P1/P2 |
| `Set-AzurePrivilegedUsers` | Audita gli account privilegiati | Permessi Global Admin |

### Opzioni di Deployment Enterprise

| Metodo | Caso d'Uso | Requisiti |
|--------|----------|--------------|
| **Esecuzione Diretta** | Testing, ambienti piccoli | Diritti admin locali |
| **Group Policy** | Ambienti di dominio | Admin di dominio, gestione GP |
| **Microsoft Intune** | Dispositivi gestiti nel cloud | Licenze Intune, Graph API |

## 🚀 Avvio Rapido

### Valutazione della Sicurezza
```powershell
# Carica il modulo Ghost
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Controlla la postura di sicurezza attuale
Get-Ghost
```

### Hardening di Base (Testa Prima)
```powershell
# Hardening essenziale - testa in ambiente lab prima
Set-Ghost -SMBv1 -AutoRun -Macros

# Rivedi le modifiche
Get-Ghost
```

### Deployment Enterprise
```powershell
# Deployment Group Policy (ambienti di dominio)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Deployment Intune (dispositivi gestiti nel cloud)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Metodi di Installazione

### Opzione 1: Download Diretto (Testing)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Opzione 2: Installazione Modulo
```powershell
# Installa da PowerShell Gallery (quando disponibile)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Opzione 3: Deployment Enterprise
```powershell
# Copia in posizione di rete per deployment Group Policy
# Configura script PowerShell Intune per deployment cloud
```

## 💼 Esempi di Casi d'Uso

### Piccola Impresa
```powershell
# Protezione di base con impatto minimo
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Ambiente Sanitario
```powershell
# Hardening focalizzato su HIPAA
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Servizi Finanziari
```powershell
# Configurazione ad alta sicurezza
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Organizzazione Cloud-First
```powershell
# Deployment gestito da Intune
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Dettagli delle Funzioni

### Funzioni di Hardening Core

#### Servizi di Rete
- **RDP**: Blocca l'accesso remote desktop o randomizza la porta
- **SMBv1**: Disabilita il protocollo di condivisione file legacy
- **ICMP**: Previene le risposte ping per ricognizione
- **LLMNR/NetBIOS**: Blocca i protocolli di risoluzione nomi legacy

#### Sicurezza Applicazioni  
- **Macro**: Disabilita l'esecuzione delle macro nelle applicazioni Office
- **AutoRun**: Previene l'esecuzione automatica da media rimovibili

#### Gestione Remota
- **PSRemoting**: Disabilita le sessioni PowerShell remote
- **WinRM**: Ferma Windows Remote Management
- **Remote Assistance**: Blocca le connessioni di assistenza remota

#### Controllo Accessi
- **Admin Shares**: Disabilita le condivisioni C$, ADMIN$
- **Guest Account**: Disabilita l'accesso account Guest
- **USB Storage**: Limita l'uso dei dispositivi USB

### Integrazione Azure
```powershell
# Connetti al tenant Azure
Connect-AzureGhost -Interactive

# Abilita i default di sicurezza
Set-AzureSecurityDefaults -Enable

# Configura accesso condizionale
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Audita utenti privilegiati
Set-AzurePrivilegedUsers -AuditOnly
```

### Integrazione Intune (Nuovo in v2)
```powershell
# Connetti a Intune
Connect-IntuneGhost -Interactive

# Deploy tramite policy Intune
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Considerazioni Importanti

### Requisiti di Testing
- **Ambiente Lab**: Testa tutte le impostazioni in ambiente isolato prima
- **Deployment Graduale**: Implementa gradualmente per identificare problemi
- **Piano di Rollback**: Assicurati di poter invertire le modifiche se necessario
- **Documentazione**: Registra quali impostazioni funzionano per il tuo ambiente

### Impatto Potenziale
- **Produttività Utente**: Alcune impostazioni possono influire sui flussi di lavoro giornalieri
- **Applicazioni Legacy**: I sistemi più vecchi potrebbero richiedere certi protocolli
- **Accesso Remoto**: Considera l'impatto sull'amministrazione remota legittima
- **Processi Aziendali**: Verifica che le impostazioni non compromettano funzioni critiche

### Limitazioni di Sicurezza
- **Difesa in Profondità**: Ghost è uno strato di sicurezza, non una soluzione completa
- **Gestione Continua**: La sicurezza richiede monitoraggio e aggiornamenti continui
- **Training Utenti**: I controlli tecnici devono essere abbinati alla consapevolezza di sicurezza
- **Evoluzione delle Minacce**: I nuovi metodi di attacco possono aggirare le protezioni attuali

## 🎯 Esempi di Scenari di Attacco

Mentre Ghost prende di mira i vettori di attacco comuni, la prevenzione specifica dipende dall'implementazione e testing appropriati:

### Attacchi Stile WannaCry
- **Mitigazione**: `Set-Ghost -SMBv1` disabilita il protocollo vulnerabile
- **Considerazione**: Assicurarsi che nessun sistema legacy richieda SMBv1

### Ransomware Basato su RDP
- **Mitigazione**: `Set-Ghost -RDP` blocca l'accesso remote desktop
- **Considerazione**: Potrebbe richiedere metodi di accesso remoto alternativi

### Malware Basato su Documenti
- **Mitigazione**: `Set-Ghost -Macros` disabilita l'esecuzione delle macro
- **Considerazione**: Può influire sui documenti legittimi abilitati alle macro

### Minacce Trasmesse via USB
- **Mitigazione**: `Set-Ghost -USBStorage -AutoRun` limita la funzionalità USB
- **Considerazione**: Può influire sull'uso legittimo dei dispositivi USB

## 🏢 Funzionalità Enterprise

### Supporto Group Policy
```powershell
# Applica impostazioni tramite registry Group Policy
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Le impostazioni si applicano a livello di dominio dopo il refresh GP
gpupdate /force
```

### Integrazione Microsoft Intune
```powershell
# Crea policy Intune per le impostazioni Ghost
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Le policy si distribuiscono automaticamente ai dispositivi gestiti
```

### Reporting di Conformità
```powershell
# Genera report di valutazione sicurezza
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Report postura sicurezza Azure
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Best Practice

### Pre-Deployment
1. **Documenta Stato Attuale**: Esegui `Get-Ghost` prima delle modifiche
2. **Testa Accuratamente**: Valida in ambiente non di produzione
3. **Pianifica Rollback**: Sappi come invertire ogni impostazione
4. **Revisione Stakeholder**: Assicurati che le unità aziendali approvino le modifiche

### Durante il Deployment
1. **Approccio Graduale**: Deploy prima sui gruppi pilota
2. **Monitora Impatto**: Osserva reclami utenti o problemi di sistema
3. **Documenta Problemi**: Registra eventuali problemi per riferimento futuro
4. **Comunica Modifiche**: Informa gli utenti sui miglioramenti di sicurezza

### Post-Deployment
1. **Valutazione Regolare**: Esegui `Get-Ghost` periodicamente per verificare le impostazioni
2. **Aggiorna Documentazione**: Mantieni aggiornate le configurazioni di sicurezza
3. **Rivedi Efficacia**: Monitora gli incidenti di sicurezza
4. **Miglioramento Continuo**: Regola le impostazioni basandoti sul panorama delle minacce

## 🔧 Risoluzione Problemi

### Problemi Comuni
- **Errori di Permessi**: Assicurati che la sessione PowerShell sia elevata
- **Dipendenze Servizi**: Alcuni servizi potrebbero avere dipendenze
- **Compatibilità Applicazioni**: Testa con le applicazioni aziendali
- **Connettività di Rete**: Verifica che l'accesso remoto funzioni ancora

### Opzioni di Ripristino
```powershell
# Riabilita servizi specifici se necessario
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 Informazioni sull'Autore

**Jim Tyler** - Microsoft MVP per PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10.000+ iscritti)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Intelligence di sicurezza settimanale
- **Autore**: "PowerShell for Systems Engineers"
- **Esperienza**: Decenni di automazione PowerShell e sicurezza Windows

## 📄 Licenza e Disclaimer

### Licenza MIT
Ghost è fornito sotto Licenza MIT per uso, modifica e distribuzione gratuiti.

### Disclaimer di Sicurezza
- **Nessuna Garanzia**: Ghost è fornito "così com'è" senza garanzie di alcun tipo
- **Testing Richiesto**: Testa sempre in ambienti non di produzione prima
- **Guida Professionale**: Consulta professionisti della sicurezza per deployment di produzione
- **Impatto Operativo**: Gli autori non sono responsabili per interruzioni operative
- **Sicurezza Completa**: Ghost è un componente di una strategia di sicurezza completa

### Supporto
- **GitHub Issues**: [Segnala bug o richiedi funzionalità](https://github.com/jimrtyler/Ghost/issues)
- **Documentazione**: Usa `Get-Help <function> -Full` per aiuto dettagliato
- **Community**: Forum della community PowerShell e sicurezza

---

**🔒 Rafforza la tua postura di sicurezza con Ghost - ma testa sempre prima.**

```powershell
# Inizia con la valutazione, non con le assunzioni
Get-Ghost
```

**⭐ Aggiungi una stella a questo repository se Ghost aiuta a migliorare la tua postura di sicurezza!**