# Tictactrip Back End API

This is an API created for Tictactrip technical tests

## Installing

```
npm install
npm start
```

The local server run on port 5000
The public server will be communicated through email.

## Infos

| Credentials       | Value  |
| ------------- | :-----|
| **email**      |  tictac@trip.com |
| **password**      |  voyage2020 |


## Endpoints

- [Token](#Token)
- [Justify](#Justify)

---

## Token

Used to get an access Token for a registered User.

**URL** : `/api/token`

**Method** : `POST`

**Headers** : `Content-Type: application/json`

**Data constraints**

```json
{
    "email": "[valid email]",
    "password": "[password in plain text]"
}
```

#### Success Response

A token to access api service justify endpoints

**Code** : `200 OK`

**Content example**

```json
{
    "accessToken": "eyJhbGciAzJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRpY3RhY0B0cmlwLmNvbSIsInBhc3N3b3JkIjoiJDJhJDA4JE1Nc2tTR2w1YUxFbVZzemNtc3d4d08xVjMueUVXMzkwbmliZFFjckKZukZqcDA2ckxUTWRxIiwiaWF0IjoxNjAyNjc3OTM0fQ.s-T2W58zI7saaTxKwVXY4SqsbTKUphRdB4KccoH08Bs"
}
```

#### Error Response


**Condition** : Something get wrong with the request.

**Code** : `400 BAD REQUEST : Invalid login credentials`


---


## Justify

Get a justified text

**URL** : `/api/justify`

**Method** : `POST`

**Auth required** : Authorization header with Bearer token

**Headers** : `Content-Type: application/json`

**Body** : `raw`

#### Success Response

**Code** : `200 OK`

**Content example**

```plain text
	Longtemps, je me suis couché de bonne heure. Parfois, à peine ma bougie éteinte,
	mes  yeux  se  fermaient  si  vite  que  je n’avais pas le temps de me dire: «Je
	m’endors.»  Et, une demi-heure après, la pensée qu’il était temps de chercher le
```

#### Error Response

**Condition** : If access token is wrong.

**Code** : `400 Bad Request`

**Message** : `User doesn't exist with the email : ****@****.***`

**Condition** : If the word's count excess 80 000 words

**Code** : `402 Payment Required`

**Message** : `Payment Required`

---


Détail des tâches à effectuer :

1. Justifier les lignes d'un string tous les 80 chars : ok
2. Créer une méthode d'authentification utilisateur
	2.a L'utilisateur envoie requête post avec un un json body {"email":"foo@bar.com"} sur la route /api/token : ok
	2.b L'utilisateur reçoit un token unique : ok
	2.c Chaque jour, l'utilisateur possède un total de 80 000 mots justifiable

3. L'utilisateur envoie axios.post son token + le text sur la route /api/justify
	3.a L'api check en fonction du jour, du token de l'user et de son email s'il peut justifier son string
	3.b Cas ok : Renvoie un string justifié tous les 80 chars : ok
	3.c Cas ko : Renvoie status code 402 : Payment Required : ok

4. Implémenter des tests unitaire

5. Documenter l'application