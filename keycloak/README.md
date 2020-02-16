## ベース
[Keycloakを使って、GrowiのSAML認証を使ってみた](https://qiita.com/sahya/items/d8ad66aadcf587c6f0a3)を参考.

## Keycloak側の設定
Keycloak側の設定はKeycloakに入って`/bin/setup-saml.sh`を実行すればOK.

## GROWI側の設定
上記で作成したGROWIレルムの情報は[ここ](http://localhost:8080/auth/realms/GROWI/protocol/saml/descriptor)でXML形式で見れる.

GROWI側の設定はdev/env.jsには以下を追加すればOK.
```
  SAML_USES_ONLY_ENV_VARS_FOR_SOME_OPTIONS: true,
  SAML_ENABLED: true,
  SAML_ENTRY_POINT: 'http://localhost:8080/auth/realms/GROWI/protocol/saml',
  SAML_ISSUER: 'localhost:3000',
  SAML_ATTR_MAPPING_ID: "id",
  SAML_ATTR_MAPPING_USERNAME: "username",
  SAML_ATTR_MAPPING_MAIL: "email",
  SAML_ATTR_MAPPING_FIRST_NAME: "firstName",
  SAML_ATTR_MAPPING_LAST_NAME: "lastName",
  SAML_CERT: '<上記のコマンドの最後に出力された証明書を入れる>'
```