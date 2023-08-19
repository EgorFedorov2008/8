from django.contrib import admin
from django.contrib.admin import AdminSite
from .models import Advertisement


class AdvertisementAdmin(admin.ModelAdmin):
    list_display = ["id", "title", "description", "price", "created_at", "auctions"]
    list_filter = ["created_at", "auctions"]


admin.site.register(Advertisement, AdvertisementAdmin)


class Title(AdminSite):
    site_title = "Обьект"


@admin.display(description="дата создания")
def created_date(self):
    from django.utils import timezone
    from django.utils.html import format_html

    if self.created_at.date() == timezone.now().date():
        created_time = self.created_at.time().strftime("%H:%M:%S")
        return format_html(
            "<span style="color: green; font-weight: bold;">Сегодня в {}</span>",
        
        )
        return self.created_at.strftime("%d.%m.%Y в %H:%M:%S")


@admin.display(description="дата обновления")


def created_date(self):
    from django.utils import timezone
    from django.utils.html import format_html

    if self.updated_at.date() == timezone.now().date():
        updated_time = self.updated_at_at.time().strftime("%H:%M:%S")
        return format_html(
            "<span style="color: green;font - weight: bold;">Сегодня в {}</span>",

        )
        return self.updated_at.strftime("%d.%m.%Y в %H:%M:%S")


@admin.display
class Book(models.Model):
    title = models.CharField(max_length=150)
    cover = models.ImageField(upload_to='adv.png')
    book = models.FileField(upload_to='adv.png')

    def __str__(self):
        return self.title
@admin.display
