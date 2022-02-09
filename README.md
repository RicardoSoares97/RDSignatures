
# RDSignatures

Assinatura de XML's com Cartão da Ordem e Cartão de Cidadão em C#

Possível:
- Autenticação
- Assinatura Digital


## Instalar

Instalar via NuGet Gallery
https://www.nuget.org/packages/RDSignatures/1.0.0?_src=template

```bash
  Install-Package RDSignatures -Version 1.0.0
```
    
## Como utilizar

1) Primeira Etapa
- Necessário obter o certificado "pai" e "filho" para efetuar tanto a autenticação e assinatura

Exemplo:

    //obter o certificado de autenticacao "pai" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certRoot = RDSignaturesClass.ReturnCertificate(true, true, "Ricardo Manuel Patrício Soares");
    
    //obter o certificado de autenticacao "filho" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certChild = RDSignaturesClass.ReturnCertificate(false, true, "Ricardo Manuel Patrício Soares");

2) Segunda Etapa
- Necessário enviar o XML em string e os certificados obtidos na primeira etapa, necessário ainda enviar o tipo de CanonicalizationMethod e SignatureMethod

Exemplo:

    //obter o SignedXml com os parametros necessarios para preencher um request
    SignedXml xmlSignedObject = RDSignaturesClass.SignXmlFileWithCertificate(xml, certRoot, certChild, SignedXml.XmlDsigCanonicalizationWithCommentsUrl, SignedXml.XmlDsigRSASHA1Url);


## Authors

- [@RicardoSoares97](https://github.com/RicardoSoares97)


## Contactos
1) E-mail
- ricardo.18.soares@hotmail.com

2) Rede Social
- https://www.linkedin.com/in/ricardosoares97/ (Linkedin)
