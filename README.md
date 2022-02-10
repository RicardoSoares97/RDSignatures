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

Requer ainda de dois programas adicionais:

Cartão de Cidadão
- Autenticação Gov.PT - https://www.autenticacao.gov.pt/

Cartão da Ordem dos Médicos
- AWP Identity Manager - https://www.omcentro.com/cedula-profissional/nova-cedula-profissional/
## Como utilizar

1) Primeira Etapa
- Necessário obter o certificado "pai" e "filho" para efetuar tanto a autenticação e assinatura

Exemplo Autenticação CC:

    //obter o certificado de autenticacao "filho" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certChildAutenticacaoCC = RDSignaturesClass.ReturnCertificate("EC de Autenticação do Cartão de Cidadão 0017", "RICARDO MANUEL PATRÍCIO SOARES");

    //obter o certificado de autenticacao "pai" através do issuer name do certificado "filho"
    X509Certificate2 certRootAutenticacaoCC = RDSignaturesClass.ReturnCertificate(certChildAutenticacaoCC.IssuerName.Name);

Exemplo Assinatura Digital CC:

    //obter o certificado de assinatura "filho" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certChildAssinaturaCC = RDSignaturesClass.ReturnCertificate("EC de Assinatura Digital Qualificada do Cartão de Cidadão 0017", "RICARDO MANUEL PATRÍCIO SOARES");

    //obter o certificado de assinatura "pai" através do issuer name do certificado "filho"
    X509Certificate2 certRootAssinaturaCC = RDSignaturesClass.ReturnCertificate(certChildAssinaturaCC.IssuerName.Name);

Exemplo Autenticação OM:

    //obter o certificado de autenticacao "filho" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certChildAutenticacaoOM = RDSignaturesClass.ReturnCertificate("MULTICERT Trust Services Certification Authority 002", "[Autenticação] (espécimen)");

    //obter o certificado de autenticacao "pai" através do issuer name do certificado "filho"
    X509Certificate2 certRootAutenticacaoOM = RDSignaturesClass.ReturnCertificate(certChildAutenticacaoOM.IssuerName.Name);

Exemplo Assinatura Digital OM:

    //obter o certificado de assinatura "filho" através do nome que da pessoa, possível retornar NULL caso não encontre
    X509Certificate2 certChildAssinaturaOM = RDSignaturesClass.ReturnCertificate("MULTICERT Trust Services Certification Authority 002", "[Assinatura Qualificada] (espécimen)");

    //obter o certificado de assinatura "pai" através do issuer name do certificado "filho"
    X509Certificate2 certRootAssinaturaOM = RDSignaturesClass.ReturnCertificate(certChildAutenticacaoOM.IssuerName.Name);



2) Segunda Etapa
- Necessário enviar o XML em string e os certificados obtidos na primeira etapa, necessário ainda enviar o tipo de CanonicalizationMethod e SignatureMethod

Exemplo:

    //obter o SignedXml com os parametros necessarios para preencher um request
    SignedXml xmlSignedObject = RDSignaturesClass.SignXmlFileWithCertificate(xml, certRootAutenticacaoCC, certChildAssinaturaCC, SignedXml.XmlDsigCanonicalizationWithCommentsUrl, SignedXml.XmlDsigRSASHA1Url);


## Authors

- [@RicardoSoares97](https://github.com/RicardoSoares97)


## 🔗 Links
[![email](https://img.shields.io/badge/email-Ricardo_soares-000?style=for-the-badge&logo=microsoft&logoColor=white)](mailto:ricardo.18.soares@hotmail.com)

[![linkedin](https://img.shields.io/badge/Ricardo_Soares-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ricardosoares97/)

[![github](https://img.shields.io/badge/github-autenticação_GOV.PT-3C5DBC?style=for-the-badge&logo=twitter&logoColor=white)](https://github.com/amagovpt/autenticacao.gov)
