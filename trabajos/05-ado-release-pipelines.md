## Trabajo Práctico 5 - Despliegue de aplicaciones con Azure Devops Release Pipelines

### 1- Objetivos de Aprendizaje
 - Adquirir conocimientos acerca de las herramientas de despliegue y releases de aplicaciones.
 - Configurar este tipo de herramientas.

### 2- Unidad temática que incluye este trabajo práctico
Este trabajo práctico corresponde a la unidad Nº: 3 (Libro Continuous Delivery: Cap 10)

### 3- Consignas a desarrollar en el trabajo práctico:
 - Los despliegues (deployments) de aplicaciones se pueden realizar en diferentes tipos de entornos
   - On-Premise (internos) es decir en servidores propios.
   - Nubes Públicas, ejemplo AWS, Azure, Gcloud, etc.
   - Plataformas como servicios (PaaS), ejemplo Heroku, Google App Engine, AWS, Azure, etc
 - Para este práctico utilizaremos como ejemplo a Google Cloud

### 4- Desarrollo:

## Crear una cuenta en Azure

1\. Navigate to [https://azure.microsoft.com/es-mx/](https://azure.microsoft.com/es-mx/)


2\. Click "Comenzar a usar Azure"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/c6b10b19-339c-4d02-a524-eb552d66fda4/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=558,-3)


3\. Click "Probar Azure gratis"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/ac523580-203f-4497-88c6-e2d05e20102b/ascreenshot.jpeg?tl_px=0,204&br_px=859,685&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=192,212)


4\. Click "Usar otra cuenta"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/80d9b3a9-9928-4894-8044-01fdd370471e/ascreenshot.jpeg?tl_px=269,443&br_px=1129,924&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


5\. Click this button.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/f32d5e77-531d-4364-80ef-0c8bbb379c05/ascreenshot.jpeg?tl_px=456,312&br_px=1316,793&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


6\. Click "Cree una"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/5e60ec4c-8f1e-4a79-bbd4-ce5c48057e28/ascreenshot.jpeg?tl_px=337,245&br_px=1197,726&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


7\. Click "get a new one"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/afa2e4f5-8d1e-44e1-8660-12de7d97a93e/ascreenshot.jpeg?tl_px=365,162&br_px=1225,643&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


8\. Click "Next"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/ac07a53d-3685-48a7-ad85-c52a04dabb7e/ascreenshot.jpeg?tl_px=458,336&br_px=1318,817&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


9\. Click "Next"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/1c7816d2-921b-492d-9ed2-cc1b2efc7917/ascreenshot.jpeg?tl_px=462,368&br_px=1322,849&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


10\. Click "Next"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/c8abc064-5ed4-4956-b86a-1e4b8a0c7637/ascreenshot.jpeg?tl_px=497,372&br_px=1357,853&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


11\. Click "Next"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/28558c68-72c2-4689-9d48-337ddf893843/ascreenshot.jpeg?tl_px=500,444&br_px=1360,925&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


12\. Click "To verify your email address use this security code: 399365"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/fbe2a0bd-0b90-474a-a3d3-dde4ffb0a52f/ascreenshot.jpeg?tl_px=243,172&br_px=1103,653&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


13\. Click "Next"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/56490255-84b9-4921-9819-6ab6d10edae8/ascreenshot.jpeg?tl_px=482,417&br_px=1342,898&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


14\. Click "Sign in"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/d06b46be-fb5c-454a-aac5-2091b8f84df4/ascreenshot.jpeg?tl_px=462,360&br_px=1322,841&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


15\. Click "Yes"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/b69e6757-6a9f-448f-9509-325ebef29b71/ascreenshot.jpeg?tl_px=455,341&br_px=1315,822&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


16\. Click "Acepto el contrato de cliente."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/72a45337-d58b-4413-b235-688b9b02634b/ascreenshot.jpeg?tl_px=0,286&br_px=859,767&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=227,212)


17\. Click the "Teléfono" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/54267126-b1d8-4591-8172-fd3bf32ae789/ascreenshot.jpeg?tl_px=14,96&br_px=873,577&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


18\. Click "Envíeme un mensaje de texto"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/75b93bcb-b64f-4353-9c2b-49a6c5113bd4/ascreenshot.jpeg?tl_px=0,270&br_px=859,751&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=390,212)


19\. Click "Comprobar código"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/29b45c8e-5b26-4a7b-8367-af897209302a/ascreenshot.jpeg?tl_px=0,401&br_px=859,882&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=299,212)


20\. Click "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/a2e5ee85-1a17-40c8-a1f9-fc8507276d5a/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=290,217)


21\. Click this button field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/87dc3039-4f21-4cc4-bc78-edffbb5d82e7/ascreenshot.jpeg?tl_px=0,101&br_px=859,582&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=373,212)


22\. Click this text field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/2547ec3f-0c04-4f44-9aec-0733a87eff6d/ascreenshot.jpeg?tl_px=0,356&br_px=859,837&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=359,212)


23\. Click "Registrarse"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/03b09f0c-05be-43bf-9910-df3f84044488/ascreenshot.jpeg?tl_px=116,487&br_px=976,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,361)


24\. Click "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/99adbd68-9ce5-4e97-8b40-a54f7ff5b20f/ascreenshot.jpeg?tl_px=467,431&br_px=1327,912&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


25\. Click "Regístrese para obtener Azure con los precios de pago por uso."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/e0e34b63-d502-4239-82dd-b615dc9e05c5/ascreenshot.jpeg?tl_px=423,134&br_px=1283,615&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


26\. Click "Acepto el contrato de cliente."

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/718b7a57-fa94-47ad-962f-a0a96767c8d8/ascreenshot.jpeg?tl_px=0,61&br_px=859,542&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=231,212)


27\. Click "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/6617b10e-3771-4408-bbe1-61e21124c60c/ascreenshot.jpeg?tl_px=0,286&br_px=859,767&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=294,212)


28\. Click "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/5c569c66-3721-45fe-8843-273cf8c1359a/ascreenshot.jpeg?tl_px=0,290&br_px=859,771&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=274,212)


29\. Click "Registrarse"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/7f1b810e-6dfd-4248-9ac6-6e5f10499494/ascreenshot.jpeg?tl_px=28,487&br_px=887,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,361)


30\. Click "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/62c8a8b0-2a17-452f-80b0-f0267bb9bb53/ascreenshot.jpeg?tl_px=469,441&br_px=1329,922&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


31\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/84c7cb19-c812-44a4-9dec-d68c0be415e0/ascreenshot.jpeg?tl_px=454,256&br_px=1314,737&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


32\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/13d09b79-3b01-4c5b-85ee-3c9e5ab7fc63/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=134,137)


33\. Click "Verify"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/a0abf4e1-adf8-4b58-bf0a-60c917564c77/ascreenshot.jpeg?tl_px=466,373&br_px=1326,854&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


34\. Click "[azportal2024@gmail.com](mailto:azportal2024@gmail.com)"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/a52e29ff-3449-48e5-a598-5f0b4c6885cb/ascreenshot.jpeg?tl_px=338,125&br_px=1198,606&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


35\. Click this icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-08-29/35588b40-0ab1-4a69-bf1e-6f8738eafd30/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=808,42)


# Crear un recurso Web App en Azure Portal

1\. Navigate to [https://portal.azure.com/#home](https://portal.azure.com/#home)


2\. Click this icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/699d7c93-5e30-40b0-a784-bb232bbeef4c/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=264,115)


3\. Click the "Buscar servicios y marketplace" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/477981f4-6ee2-48c3-9261-97b59fe2b635/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=348,125)


4\. Click this image.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a7944fc4-82ba-4c2e-a29e-569b5aa921dd/ascreenshot.jpeg?tl_px=681,119&br_px=1541,600&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=432,212)


5\. Click "Planes"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/d91bb0c2-afbb-47b9-93eb-f955a67052f4/ascreenshot.jpeg?tl_px=0,151&br_px=859,632&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=176,212)


6\. Click "Información de uso y soporte técnico"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/79fcfefb-3d2f-4472-b42b-42ff1c5195c7/ascreenshot.jpeg?tl_px=0,147&br_px=859,628&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=296,212)


7\. Click "Crear"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a0fb8565-6a6a-4e9e-965a-a611ccc7de29/ascreenshot.jpeg?tl_px=0,48&br_px=859,529&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=389,212)


8\. Click "(Nuevo) Grupo de recursos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/2791e4a8-db6d-4896-8868-467108714fb9/ascreenshot.jpeg?tl_px=0,176&br_px=859,657&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=353,212)


9\. Click "(Nuevo) Grupo de recursos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/d9b09799-ea72-4540-bbcc-a6f990abbc2d/ascreenshot.jpeg?tl_px=0,168&br_px=859,649&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=350,212)


10\. Click "Crear nuevo"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/4c2d2cc6-716d-4a43-940e-06155eb3c6fa/ascreenshot.jpeg?tl_px=0,198&br_px=859,679&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=304,212)


11\. Type "TPSIngSoft3UCC2024"


12\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/f3d93ccc-201a-47c4-8036-d2f1447d4885/ascreenshot.jpeg?tl_px=0,371&br_px=859,852&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=342,212)


13\. Click the "Nombre" field.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/74ca7403-ac4c-4401-8b96-6973cdda1f40/ascreenshot.jpeg?tl_px=0,281&br_px=859,762&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=397,212)


14\. Type "MiWebApp01"


15\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/d5687ed0-9f00-4f8f-9f62-ee4c5f8a1338/ascreenshot.jpeg?tl_px=0,327&br_px=859,808&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=273,212)


16\. Click "Seleccione una pila del entorno en tiempo de ejecución"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/b36e2e59-cf3d-49d1-b9ca-15952ab57e4d/ascreenshot.jpeg?tl_px=0,421&br_px=859,902&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=371,212)


17\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/0a8973c1-da85-4a4f-bfff-013d94d056a3/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=352,187)


18\. Click "Estándar S1 (Total de ACU: 100, 1.75 GB de memoria, 1 vCPU)"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/5072c787-029a-43dc-a5c7-abfae4e86271/ascreenshot.jpeg?tl_px=0,448&br_px=859,929&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=374,212)


19\. Click "60 minutos de CPU/día incluidos"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/e74b0a6b-6e32-4dbe-b801-24dcd7612c75/ascreenshot.jpeg?tl_px=3,79&br_px=862,560&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


20\. Click "Crear nuevo"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/abd461a8-c319-4a32-80ba-4560a296f5f0/ascreenshot.jpeg?tl_px=0,338&br_px=859,819&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=303,212)


21\. Type "MiAppPlan01"


22\. Click "Aceptar"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/2ce05660-43b4-403a-84ea-a49738fc066a/ascreenshot.jpeg?tl_px=0,476&br_px=859,957&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=328,212)


23\. Click "Siguiente: Base de datos >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/3e6e97a1-2cae-4aa2-b3db-3d7b7aac6d54/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=323,411)


24\. Click "Siguiente: Implementación >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/4440896d-cc16-4e3d-937e-ced647c789a0/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=339,421)


25\. Click "Deshabilitar"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/fc5e4758-8230-46dd-a4c0-9b0fc1bfe82f/ascreenshot.jpeg?tl_px=0,47&br_px=859,528&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=295,212)


26\. Click "Siguiente: Redes >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/ed6fd2e0-5c15-484b-99cd-3509e5c359aa/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=345,423)


27\. Click "Siguiente: Supervisión y protección >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/6a9471d7-b0fc-46d0-92de-8618bff28d05/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=389,420)


28\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/51e65a51-2a51-44d9-acd2-ddde9c4cb4b4/ascreenshot.jpeg?tl_px=0,176&br_px=859,657&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=265,212)


29\. Click "Siguiente: Etiquetas >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/2008e818-fbb7-4b9d-b0ba-9bd2f25963e2/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=319,416)


30\. Click "Siguiente: Revisar y crear >"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/b36b996a-0746-42c6-b8f5-900a98fec43b/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=349,424)


31\. Click "Descargar una plantilla para la automatización"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/23e9fc9f-f718-41a7-96c0-bc9a74c4d469/ascreenshot.jpeg?tl_px=29,487&br_px=888,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,423)


32\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/e53fc21f-5705-4e03-8e7a-1d94e6d92222/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=74,122)


33\. Click "Crear"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/9dccaabe-c69a-489b-89aa-5a77c551cf7f/ascreenshot.jpeg?tl_px=0,487&br_px=859,968&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=42,419)


34\. Click this icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/aaf4fc77-d72b-4d8a-bffb-86bfd549890d/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=484,-7)


35\. Click "Ir al recurso"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a2151089-bcdd-454e-972c-0848d573ddb0/ascreenshot.jpeg?tl_px=0,241&br_px=859,722&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=378,212)


36\. Click this icon.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/5077baf7-20b0-4f24-8c45-80806b044ccf/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=791,34)


37\. Click "[miwebapp01.azurewebsites.net](http://miwebapp01.azurewebsites.net)"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a250a47b-4fa8-4a28-a200-dce85d724a23/ascreenshot.jpeg?tl_px=681,17&br_px=1541,498&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=431,212)


38\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/57cc8aa4-cde7-444c-8c40-b9f15a32e76c/ascreenshot.jpeg?


## Crear un Pipeline de Release en Azure DevOps

1\. Navegar a [https://dev.azure.com/](https://dev.azure.com/azportal2024/Sample01)NOMBRE_DE_TU_ORGANIZACION


2\. Seleccionar el Proyecto deseado


3\. Click "Pipelines"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/10bfa9ac-c36c-4411-b517-f45b2d5f165f/ascreenshot.jpeg?tl_px=0,143&br_px=859,624&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=83,212)


4\. Click "Releases"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/f71931be-da25-48b1-af65-0663113baf8d/ascreenshot.jpeg?tl_px=0,155&br_px=859,636&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=85,212)


5\. Click "New pipeline"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/556f67d2-c5f2-4624-ac84-22c94661711e/ascreenshot.jpeg?tl_px=482,267&br_px=1342,748&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


6\. Seleccionar template "Azure App Service Deployment" y click en "Apply"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/610cdcbb-c913-40b9-b87d-9d9c24a00880/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=747,199)


7\. Cambiar el nombre de la etapa a "Deploy a QA"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/e19d9ccf-b556-48d2-9f8f-3a00a7737863/ascreenshot.jpeg?tl_px=681,94&br_px=1541,575&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=420,212)


8\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/509b054f-6498-45f6-a8ec-1bd72c6f970f/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=816,129)


9\. Agregar el artefacto a deployear, es el resultado del pipeline de build. Click en "Add"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a1915d11-b8d6-44b7-8c0c-dcf46530b305/ascreenshot.jpeg?tl_px=17,0&br_px=877,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,189)


10\. Seleccionamos el proyecto (por defecto el proyecto en el que estamos) y seleccionamos el pipeline del cual queremos sacar el artefacto a deployear. Click en "Expand"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/39cc8234-57b2-4e2b-823d-82980637b6f1/ascreenshot.jpeg?tl_px=681,160&br_px=1541,641&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=771,212)


11\. Click en el nombre de nuestro pipeline

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/4b7dd169-a457-4b37-a9fa-588edffd70c4/ascreenshot.jpeg?tl_px=681,193&br_px=1541,674&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=566,212)


12\. Click "Add"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/cf87276c-4e51-4837-a7ec-b25b95deba0f/ascreenshot.jpeg?tl_px=536,433&br_px=1396,914&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


13\. Habilitamos Continuous Deployment, cada vez que el pipeline de build se ejecute exitosamente, se disparará este pipeline de release.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/6514f4d1-91a4-4ee8-8d47-f637f3efa17b/ascreenshot.jpeg?tl_px=31,47&br_px=890,528&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


14\. Habilitamos el toggle dejandolo **Habilitado**

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/e222b441-b840-4afb-bf1e-9bd27c5204d0/ascreenshot.jpeg?tl_px=498,6&br_px=1358,487&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


15\. Configuramos las tareas del stage. Click "1 job, 1 task"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/70a7bffa-dd25-416e-abd0-fddc69097ec4/ascreenshot.jpeg?tl_px=275,97&br_px=1135,578&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


16\. Buscamos nuestra suscripción creada en Azure Portal. Click "Expand"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/3270900a-3e9d-494e-bf0f-17904e91ff36/ascreenshot.jpeg?tl_px=681,62&br_px=1541,543&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=746,212)


17\. Seleccionamos nuestra suscripción.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/829c7cc7-fffc-45cc-8c38-2420a1219fff/ascreenshot.jpeg?tl_px=681,159&br_px=1541,640&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=645,212)


18\. Click "Authorize". Nos pedirá nuestros datos de la cuenta de Azure Portal

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/cf53903b-a799-426b-9301-55945b4037a6/ascreenshot.jpeg?tl_px=681,61&br_px=1541,542&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=691,212)


19\. Ingresamos nuestra cuenta de Azure Portal y hacemos click en "Siguiente"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/9af18179-fcf7-48c4-972f-bb9efd871973/ascreenshot.jpeg?tl_px=100,90&br_px=960,571&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=482,212)


20\. Click "Send code"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/d2d6df7b-91ca-4e41-8b6b-6e8acd31fa56/ascreenshot.jpeg?tl_px=100,118&br_px=960,599&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=487,278)


21\. Una vez recibido el código en nuestro mail, lo ingresamos y clickeamos en "Sign in"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/a4a33354-dce0-429d-b86b-e44c800dccd8/ascreenshot.jpeg?tl_px=100,118&br_px=960,599&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=468,285)


22\. Expandimos el combo para ver las opciones disponibles y dejamos seleccionada "Web App on Windows"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/4e07dfc5-5cec-4685-b30b-02bed1c62530/ascreenshot.jpeg?tl_px=681,187&br_px=1541,668&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=756,212)


23\. Expandimos el combo de App service Name y seleccionamos nuestra Web App creada en Azure Portal

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/5fb87794-6e23-470c-8faf-6e378ec76225/ascreenshot.jpeg?tl_px=681,284&br_px=1541,765&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=704,212)


24\. Click "Save"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/7c796430-b452-42e0-a2bd-2aae924fdca4/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=447,52)


25\. Click "OK"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/748513ed-d926-44da-8e6c-d8672e57486d/ascreenshot.jpeg?tl_px=451,360&br_px=1311,841&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


26\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/b0aa6a68-675a-41e4-9af4-0b1118849b8b/ascreenshot.jpeg?tl_px=183,76&br_px=1043,557&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


27\. Click "Releases"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/e667c53d-66e1-4d86-903b-d99c088f0574/ascreenshot.jpeg?tl_px=0,157&br_px=859,638&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=83,212)


28\. Seleccionamos nuestro pipeline de Release

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/1f44eebe-623a-4d46-ba80-dbbda219378f/ascreenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=396,152)


29\. Click here.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/cd6fb89c-cec9-48ab-b8dd-66c5418c00a7/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=776,107)


30\. Clickeamos en Rename para renombrar nuestro pipeline de Release

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/eb6567ff-a9b7-47f5-87a5-ab7245d01c48/ascreenshot.jpeg?tl_px=681,0&br_px=1541,480&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=656,140)


31\. Type "ReleasePipeline01"


32\. Click "OK"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2024-09-01/d8c2f803-ea8f-44a9-b99e-7b6e5b3c92b5/ascreenshot.jpeg?tl_px=558,322&br_px=1418,803&force_format=jpeg&q=100&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)





