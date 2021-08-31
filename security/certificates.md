# Certificates

## Linux : Generate certicates

Openssl.....

Instruções obtidas no Github para geração de chaves para autenticação


  1. Gera chave privada
  2. Solicita criação de certificado (CSR) usando chave privada
  3. Assina CSR utilizando CA conhecida, gerando certificado CRT
  



Criação de 
```bash

openssl req -new -newkey rsa:4096 -nodes -keyout HML_S4_serverVoiter.key -out HML_S4_serverVoiter.csr -nodes -subj "/C=BR/ST=Sao Paulo/L=Sao Paulo/O=Banco Voiter/CN=internal.obapi-hml.voiter.com"

openssl req -new -newkey rsa:4096 -nodes -keyout HML_V4_clientVoiter.key -out HML_V4_clientVoiter.csr -nodes -subj "/C=BR/ST=Sao Paulo/L=Sao Paulo/O=Banco Voiter/CN=cliente.internal.obapi-hml.voiter.com"