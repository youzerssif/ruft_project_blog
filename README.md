# ruft_project_blog

## Appllications : blog, contact, config, member, visitor, statistique

## Models de l application Blog
```python
        from django.db import models
        from tinymce import HTMLField
        from django.contrib.auth.models import User

        # Create your models here.
        class Categorie(models.Model):
            titre =  models.CharField(max_length=255)
            date_add =  models.DateTimeField(auto_now_add=True)
            date_update =  models.DateTimeField(auto_now=True)
            status =  models.BooleanField(default=True)


            def __str__(self):
                return self.titre

            class Meta:
                verbose_name = 'Categorie'
                verbose_name_plural = 'Categories'



        class Tags(models.Model):
            titre = models.CharField(max_length=250)
            status = models.BooleanField(default=True)
            date_add = models.DateTimeField(auto_now_add=True)
            date_upd = models.DateTimeField(auto_now=True)

            def __str__(self):
                return self.titre

            class Meta:
                verbose_name = 'Tags'
                verbose_name_plural = 'Tags'


        class Auteur(models.Model):
            auteur = models.OneToOneField(User,on_delete= models.CASCADE,related_name="auteur")
            image = models.ImageField(upload_to='image_auteur')
            description = models.TextField()
            status = models.BooleanField(default=True)
            date_add = models.DateTimeField(auto_now_add=True)
            date_upd = models.DateTimeField(auto_now=True)

            def __str__(self):
                    return self.auteur.username

            class Meta:

                verbose_name = 'Auteur'
                verbose_name_plural = 'Auteurs'   



        class Article(models.Model):
            auteur = models.ForeignKey(Auteur,on_delete= models.CASCADE, related_name="Auteur_article")
            titre = models.CharField(max_length=250)
            categorie_id =  models.ForeignKey(Categorie,on_delete=models.CASCADE, related_name="categorie_article")
            description =  HTMLField('description')
            contenue = HTMLField('contenue')
            tag = models.ManyToManyField(Tags,related_name="article_tag")
            slug = models.SlugField(unique=True)
            date_add =  models.DateTimeField(auto_now_add=True)
            date_update =  models.DateTimeField(auto_now=True)
            status =  models.BooleanField(default=True)
            image = models.ImageField(upload_to ='article_image', blank=True)


            def __str__(self):
                    return self.titre

            class Meta:

                verbose_name = 'Article'
                verbose_name_plural = 'Articles'


        class Commentaire(models.Model):
            """Model definition for Commentaire."""
            article = models.ForeignKey(Article,on_delete= models.CASCADE, related_name="article_commenter")
            nom = models.CharField(max_length=160)
            email = models.EmailField(max_length=254)
            website = models.URLField(max_length=200, null=True, blank=True)
            photo = models.ImageField(upload_to='commentaire_photo',default='useravatar.png')
            message = models.TextField()
            date_add =  models.DateTimeField(auto_now_add=True)
            date_update =  models.DateTimeField(auto_now=True)
            status =  models.BooleanField(default=True)

            class Meta:
                """Meta definition for Commentaire."""

                verbose_name = 'Commentaire'
                verbose_name_plural = 'Commentaires'

            def __str__(self):
                """Unicode representation of Commentaire."""

                return self.nom


        class Appreciation(models.Model):
             """Model definition for Appreciation."""

            like = models.BooleanField(default=False)
            dislike = models.BooleanField(default=False)
            article = models.ForeignKey(Article,on_delete= models.CASCADE, related_name="article_like")
            date_add =  models.DateTimeField(auto_now_add=True)
            date_update =  models.DateTimeField(auto_now=True)
            status =  models.BooleanField(default=True)

             class Meta:
                 """Meta definition for Appreciation."""

                 verbose_name = 'Appreciation'
                 verbose_name_plural = 'Appreciations'
 


```
