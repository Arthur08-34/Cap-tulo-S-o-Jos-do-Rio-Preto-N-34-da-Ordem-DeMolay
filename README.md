# Site do Capítulo DeMolay SJRP Nº34

## Rodar localmente

Como o site usa módulos do Firebase, rode por um servidor local:

```powershell
python -m http.server 8000
```

Depois abra:

```text
http://127.0.0.1:8000
```

## Configurar Firebase

1. Crie um projeto no [Firebase Console](https://console.firebase.google.com/).
2. Adicione um app Web.
3. Copie o objeto `firebaseConfig`.
4. Cole os valores em `firebase-config.js`.

Este projeto já está configurado para o Firebase `demolay-4957d`.
5. Ative Authentication > Sign-in method > Email/password.
6. Crie um banco Cloud Firestore.
7. Publique as regras de `firestore.rules` no painel Rules do Firestore.

## Coleções usadas no Firestore

- `events`: calendário / próximas atividades.
- `officials`: oficiais do capítulo.
- `advisory`: conselho consultivo.
- `sponsors`: patrocinadores.
- `members`: DeMolays ativos e administradores.
- `petitions`: petições enviadas pelo formulário público.

O site lê `events`, `officials`, `advisory` e `sponsors` publicamente. Membros ativos podem criar novos registros nessas coleções pela área autenticada. Edição e exclusão ficam restritas aos administradores com `role: "admin"` e `status: "active"` na coleção `members`.

## Primeiro administrador

Antes do painel conseguir cadastrar outros DeMolays, crie o primeiro admin:

1. No Firebase Authentication, crie um usuário com e-mail e senha.
2. Copie o UID desse usuário.
3. No Firestore, crie o documento `members/{UID}` com:

```json
{
  "memberId": "DM34-ADMIN",
  "name": "Administrador DeMolay",
  "email": "admin@demolay.org.br",
  "role": "admin",
  "status": "active"
}
```

Depois entre pelo site com esse e-mail e senha. No painel, aba `Membros`, cadastre os DeMolays ativos com ID, nome, e-mail e senha provisória.
