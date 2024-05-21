---
title: "Portal Plugin"
excerpt: "Multiplayer portal plugin for Lyra Starter Game"
header:
  teaser: /assets/images/PortalsActive.png
sidebar:
  - title: "Features"
    text: "Replication, gameplay ability system (GAS), game feature plugin, third-person"
share: false
---

This project originally started as a test for a job interview that I decided to continue
to work on it in my free time. The project is a Game Feature plugin for the [Lyra Sample Game](https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) that adds
multiplayer portal mechanics. There are more in depth details about the project in the [repository](https://github.com/kurtw/PortalGame).
When I started this project I had never used Lyra before, so it has been quite a learning journey.
It's not perfect, but every work session I get in makes it a little bit better.
<video style="display:block; margin: auto;" width="600" controls autoplay loop>
    <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/Teleport.mov" type="video/mp4">
</video><br>

As stated above, the main feature of this plugin is the portal mechanic. While doing research I came across many
great first-person examples out in the wild, so I thought it would be fun to try to do something from the third-person
perspective.

Some pain points for me have been:

<u>The learning curve Lyra</u>

There is so much going on under the hood for Lyra that sometimes it's hard to know what to even look for when creating
something new or just troubleshooting in general. Thankfully there are a number of good resources out there.

Aside from source code, some notable resources I found are:\
[./X157](https://x157.github.io)\
[Lyra Dev Net discord](https://discord.gg/323cxWbx)\
[NanceDevDiaries](https://www.youtube.com/@nancedevdiaries)\
[Rakgul](https://www.youtube.com/@Rukgul)\
[Epic Dev Community](https://dev.epicgames.com/community/)

<u>Getting the view from each portal to look good from the third-person perspective</u>

This is still a work in progress, as noted in the repo README, because I do not like how the rendered view looks with
the most current implementation.

It's too magnified and offset.

<video style="display:block; margin: 0 auto;" width="600" controls>
    <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/PortalView_current.mov" type="video/mp4">
</video><br>

One of the options I explored, code snippet provided below, looks great until rotating the camera or moving "far enough"
away from a portal.
<video style="display:block; margin: 0 auto;" width="600" controls>
    <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/PortalView_other.mov" type="video/mp4">
</video><br>

{% highlight cpp %}
void APortal::UpdatePortalRenderRotation()
{
.
.
.

    FVector Direction = OwningController->GetPawn()->GetActorLocation() - this->GetActorLocation();
    FVector TargetLocation = GetConnectedPortal()->GetActorLocation();
                
    FVector DotProduct;
    DotProduct.X = FVector::DotProduct(Direction, this->GetActorForwardVector());
    DotProduct.Y = FVector::DotProduct(Direction, this->GetActorRightVector());
    DotProduct.Z = FVector::DotProduct(Direction, this->GetActorUpVector());
                
    FVector NewDirection = DotProduct.X * -GetConnectedPortal()->GetActorForwardVector()
            + DotProduct.Y * -GetConnectedPortal()->GetActorRightVector()
            + DotProduct.Z * GetConnectedPortal()->GetActorUpVector();
                
    FVector NewLocation = TargetLocation + NewDirection;

    .
    .
    .

    UpdatePortalClipPlane(this, GetConnectedPortal());
    
    .
    .
    .
}
{% endhighlight %}<br>

{% highlight cpp %}
void APortal::UpdatePortalClipPlane(APortal* Current, APortal* Connected)
{
Connected->PortalCaptureComponent->ClipPlaneNormal = Connected->GetActorForwardVector();
Connected->PortalCaptureComponent->ClipPlaneBase = Connected->GetActorLocation() + (Current->PortalCaptureComponent->ClipPlaneNormal * -ClipModifier);
}
{% endhighlight %}<br>
My current best guess is that either NewDirection, UpdatePortalClipPlane, or both need to account for the player
location in a way that keep the portal view from clipping through the floor as seen in the video above.

<u>Niagara effect flickering</u>

At least on macOS, the Niagara effects do not play well once the portals are spawned. The effects have intense
flickering. My current solution is to disable rendering for the Niagara system attched to the B_WeaponSpawner
and BP_ExperienceList3D.
<video style="display:block; margin: 0 auto;" width="600" controls>
    <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/NiagaraFlicker.mov" type="video/mp4">
</video>