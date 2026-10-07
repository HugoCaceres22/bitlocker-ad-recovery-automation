# BitLocker Recovery Key Management with Active Directory

Proyecto para gestionar BitLocker en equipos Windows de un dominio y almacenar sus claves de recuperación en Active Directory mediante GPO y PowerShell.

## Objetivo

Centralizar la configuración de BitLocker y automatizar el backup de las Recovery Keys en Active Directory.

BitLocker se habilita manualmente en cada equipo y posteriormente una tarea programada desplegada por GPO ejecuta un script PowerShell que guarda la clave de recuperación en AD.

## Funcionamiento

```text
Active Directory
      ↓
     GPO
      ↓
Windows Client
      ↓
BitLocker + TPM
      ↓
PowerShell
      ↓
Recovery Key → Active Directory
```

## Configuración

Las GPO utilizadas permiten:

- Configurar BitLocker utilizando TPM.
- Guardar la información de recuperación en Active Directory.
- Aplicar cifrado de 256 bits.
- Configurar la recuperación de la unidad del sistema.
- Desplegar una tarea programada para ejecutar el script PowerShell.

## PowerShell

El script busca el protector `RecoveryPassword` de BitLocker y realiza el backup de la clave en Active Directory.

```powershell
manage-bde -protectors -get C: -type RecoveryPassword
```

```powershell
manage-bde -protectors -adbackup C: -id <ProtectorID>
```

También genera logs para comprobar si el proceso se ha realizado correctamente.

## Tecnologías utilizadas

- Windows Server
- Active Directory
- Group Policy
- BitLocker
- TPM
- PowerShell
- Task Scheduler
- manage-bde

## Documentación

La documentación completa del proyecto, con la configuración paso a paso y capturas, está disponible aquí:

[Ver documentación completa](./BitLocker-GPO-Documentation.pdf)
