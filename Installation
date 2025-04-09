$installer = "/i `"\Autodesk\Plugins\Konekt\Newforma Konekt Autodesk Addins Revit 2025.msi`" /quiet"
$program = "Newforma Konekt Add-ins for Autodesk products"
$version = "1.133.0"  # Versão desejada

# Caminhos onde os programas podem estar registrados
$registroPaths = @(
    "HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*",
    "HKLM:\Software\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*"
)

# Variável para armazenar o resultado da busca
$instalado = $null

# Busca otimizada: para ao encontrar a entrada desejada
foreach ($path in $registroPaths) {
    $instalado = Get-ItemProperty -Path $path -ErrorAction SilentlyContinue | 
                 Where-Object { $_.DisplayName -like "*$program*" }

    if ($instalado) { break }  # Se encontrou, para a busca
}

# Verifica se encontrou e compara a versão
if ($instalado -and $instalado.DisplayVersion -eq $version) {
    Write-Output "O NEWFORMA KONEKT VERSÃO $version JÁ ESTÁ INSTALADO!"
    return  # Sai imediatamente para evitar execuções desnecessárias
}

# Caso não esteja instalado ou esteja com versão diferente, faz a instalação
Write-Output "INSTALANDO O NEWFORMA KONEKT..."
Start-Process msiexec.exe -ArgumentList $installer -Wait -NoNewWindow
Write-Output "INSTALAÇÃO CONCLUÍDA!"
