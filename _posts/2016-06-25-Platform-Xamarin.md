---
layout: post
title: Платформозависимость на Xamarin
date: 2016-06-25 13:02
tags:
- Xamarin
- Android
- iOS
- С#
- Платформозависимость
---
## Реализация нотификаций на разных платформах: ##
Здесь нам на помощь приходит DependencyService.
Как обычно в кросс-платформенной разработке, нужно объявить интерфейс в общем проекте и реализовать его в платформо-зависимых проектах. Единственным вопросом будет «как определить, какую реализацию вызвать в каждом конкретном случае?». И тут за работу берется DependencyService, магический деятель фреймворка Xamarin. В зависимости от того, для какой платформы мы собираем проект, DependencyService подставляет необходимую реализацию вместо интерфейса.
Также стоит отметить, что для того чтобы эта магия заработала, нужно использовать аннотацию Xamarin.Forms.Dependency:

{% highlight csharp %}
[assembly: Xamarin.Forms.Dependency (typeof (NotificationHelperImpl))]
{% endhighlight %}

Например, интерфейс нотификаций, объявленный в общем проекте Xamarin Forms выглядит так:

{% highlight csharp linenos %}
namespace MedChestAssistant
{
    public interface INotificationHelper
    {
        void notify(String message);
    }
}
{% endhighlight %}


А платформо-зависимая реализация в Android-проекте выглядит так:

{% highlight csharp linenos %}
[assembly: Xamarin.Forms.Dependency (typeof (NotificationHelperImpl))]
namespace MedChestAssistant.iOS
{
    public class NotificationHelperImpl: INotificationHelper
    {
        #region INotificationHelper implementation

        public void notify (string message)
        {
            var notification = new UILocalNotification();

            // set the fire date (the date time in which it will fire)
            notification.FireDate = NSDate.FromTimeIntervalSinceNow(5);

            // configure the alert
            notification.AlertAction = "Medical Chest Reminder";
            notification.AlertBody = "Lyrica will expire in 2 days. Don't forget renew it";

            // modify the badge
            notification.ApplicationIconBadgeNumber = 1;

            // set the sound to be the default sound
            notification.SoundName = UILocalNotification.DefaultSoundName;

            // schedule it
            UIApplication.SharedApplication.ScheduleLocalNotification(notification);
        }

        #endregion

        public NotificationHelperImpl ()
        {
        }
    }
} 
{% endhighlight %}

Оригинал: <https://habrahabr.ru/company/dataart/blog/282696/>


