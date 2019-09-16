

# voyage
* **Destination**
* **Vols**
* **Compagny**
* **Billet**

## Destination

```python
class Destination(models.Model):
"""Model definition for Destination."""
pays = models.CharField(max_length=255, blank=True, null=True)
ville = models.CharField(max_length=255, blank=True, null=True)
description = models.TextField()
image = models.ImageField(upload_to='destination')
class Meta:
    """Meta definition for Destination."""
    verbose_name = "Destination"
    verbose_name_plural = "Destinations"

def __str__(self):
    """Unicode representation of Destination."""
    return self.pays+"-"+self.ville

```

## Vols


```python

class Vols(models.Model):
"""Model definition for Vols."""
name = models.CharField(max_length=255,blank=True, null=True)
prix = models.CharField(max_length=255,)
destination = models.ForeignKey(Destination,on_delete=models.CASCADE,related_name='voyage_vols')
compagny = models.ForeignKey('Compagny',on_delete=models.CASCADE,related_name='compagny_vols')

class Meta:
    """Meta definition for Vols."""
    verbose_name = "vols"
    verbose_name_plural = "vols"

def __str__(self):
    """Unicode representation of Vols."""
    return " {} {} : ${} ".format(self.name,self.destination,self.prix)

```

## Compagny

```python

class Compagny(models.Model):
"""Model definition for Compagny."""
name = models.CharField(max_length=255,)
descritpion = models.TextField()
image = models.ImageField(upload_to='compagny')
    
    

class Meta:
    """Meta definition for Compagny."""
    verbose_name = "Compagny"
    verbose_name_plural = "Compagnies"

def __str__(self):
    """Unicode representation of Billet."""
    return self.name



```


## Billet 

```python 

class Billet(models.Model):
"""Model definition for Billet."""

user = models.ForeignKey(User,on_delete=models.CASCADE,related_name='user_billet')
vols= models.ForeignKey(Vols,on_delete=models.CASCADE,related_name='vols_billet')

class Meta:
    """Meta definition for Billet."""

    verbose_name = 'Billet'
    verbose_name_plural = 'Billets'

def __str__(self):
    """Unicode representation of Billet."""
    return self.user.username +' '+ str(self.vols.destination)


```
