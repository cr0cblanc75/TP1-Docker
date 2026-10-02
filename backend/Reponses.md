## Question 1-4
Un build par étape (multistage) permet de sépraer les éléments de compilation de l'application.
Pour Java/SpringBoot, on a besoin de JDK et Maven pour compiler. Mais une fois le .jar créé on en a plus besoin. 
On peut donc demander à Docker de faire une étape build, puis ensuite de se concentrer sur l'étape Run. 