---
title: Take care of your ears
subtitle:
layout: post
tags: health
---

{: .callout-note }
Quick disclaimer: I am neither a doctor nor an expert in this field, but if this write-up helps one-person look after their hearing health just a little better, I'll consider this post worthwhile.

Hearing health is seemingly overlooked by the general population. Hearing loss is linked to a number of debilitating health issues such as cognitive decline, depression. While many causes of hearing loss are unavoidable, such as genetics, age, and accidents, there are reasonable precautions we can do to protect ourselves from avoidable sources of hearing loss. From my experience, this is not widely known or talked about.

There are three things I think are important to recognize among ourselves:

1. Noise exposure is dependent on dosage. That is, the duration you are exposed to a loud noise matters.
2. Many common places we visit expose us to unsafe noise levels.
3. Hearing loss is often permanent, and there is no known cure.

## Understanding noise exposure

Noise is typically described in decibels (dB), with louder noises having a higher decibel number. Humans do not hear all frequencies equally though. To account for this, there are different weightings applied to the decibel measurement, the most common in North America being dBA, indicating the ["A" weighting](https://en.wikipedia.org/wiki/A-weighting).

<style>
.db-chart {
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}
.db-chart li {
    background-color: var(--bg-color-2);
    padding: 0.125rem 1rem;
    list-style-type: none;
    margin: 0;
    border-radius: 200px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 0.5rem;
}
.db-chart .warning {
    background-color: var(--warning-color);
}
.db-chart .loud {
    background-color: var(--danger-color);
}
.db-chart .details {
    margin-left: auto;
    font-size: 0.8em
}
.db-chart .db {
    width: 4rem;
}
</style>

<ul class="db-chart">
  <li data-decibel="140" class="loud">
    <span class="db">140dB</span>
    <span>
        Rocket launch
    </span>
    <div class="details">
        <span>⛔ Not safe</span>
    </div>
  </li>
  <li data-decibel="130" class="loud">
    <span class="db">130dB</span>
    <span>
        Jet engine
    </span>
    <div class="details">
        <span>⛔ Not safe</span>
    </div>
  </li>
  <li data-decibel="120" class="loud">
    <span class="db">120dB</span>
    <span>
        Emergency vehicle sirens
    </span>
    <div class="details">
        <span>⛔ Not safe</span>
    </div>
  </li>
  <li data-decibel="110" class="warning">
    <span class="db">110dB</span>
    <span>
        Trombone
    </span>
    <div class="details">
        <span>⚠️ 2 minutes</span>
    </div>
  </li>
  <li data-decibel="100" class="warning">
    <span class="db">100dB</span>
    <span>
        Helicopter
    </span>
    <div class="details">
        <span>⚠️ 15 minutes</span>
    </div>
  </li>
  <li data-decibel="90" class="warning">
    <span class="db">90dB</span>
    <span>
        Hair dryer
    </span>
    <div class="details">
        <span>⚠️ 2 hours</span>
    </div>
  </li>
  <li data-decibel="80" class="warning">
    <span class="db">80dB</span>
    <span>
        Truck
    </span>
    <div class="details">
        <span>⚠️ 16 hours</span>
    </div>
  </li>
  <li data-decibel="70">
    <span class="db">70dB</span>
    <span>
        Vacuum cleaner
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="60">
    <span class="db">60dB</span>
    <span>
        Conversation
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="50">
    <span class="db">50dB</span>
    <span>
        Rain
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="40">
    <span class="db">40dB</span>
    <span>
        Refrigerator
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="30">
    <span class="db">30dB</span>
    <span>
        Whisper
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="20">
    <span class="db">20dB</span>
    <span>
        Leaves
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="10">
    <span class="db">10dB</span>
    <span>
        Breathing
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
  <li data-decibel="1">
    <span class="db">1dB</span>
    <span>
        Silence
    </span>
    <div class="details">
        <span>🟢 Safe</span>
    </div>
  </li>
</ul>

<script>
Array.from(document.querySelectorAll('.db-chart li')).forEach((listItem, index) => {
  const db = parseInt(listItem.dataset.decibel, 10);
  const addedWidth =  Math.pow(db / 140, 3) ;
  const percent = (.3 + addedWidth * .7) * 100;
  listItem.style.width = `${percent}%`;
});
</script>

Notable places where I've experienced noise reaching unsafe levels:

- Commute (NYC Subway, construction, emergency vehicle sirens)
- Restaurants and bars
- Movie theaters
- Amusement park rides and shows
- Weddings
- Concerts

## What you can do

I've [configured my Apple Watch](https://support.apple.com/guide/watch/noise-apd00a43a9cb/watchos) to notify me if sound levels reach unsafe levels and I have an always-on decibel reader on my watch face so I can know at a glance what the ambient levels are.

I keep a pair of earplugs on my keychain. If I find myself unexpectedly in a loud bar I can put them in and continue to enjoy my time there without having to be so concerned about my hearing.

Wearing ear plugs: there are mainly two kinds of ear-plugs, there are those designed to block out loud sounds as much as possible, such as on construction sites and shooting ranges. There are then those that are designed to _reduce_ levels but minimally altering the sound while doing-so. These are more expensive but are better for concerts, events, movie theaters, and bars.

Wearing high-end noise cancelling headphones can reduce slightly elevated noisy environments to safe-levels. It's important that we don't just _replace_ the sounds by then playing music at unsafe levels, but this is a great tool for commuting even if imperfect.

## Closing

On a positive note, hearing loss accommodation, accessibility, medical technology and prevention tools have never been better.

However, we should of course be taking reasonable precautions to not subject ourselves to avoidable causes of hearing loss from exposure.

---

- [Hearing loss - NHS](https://www.nhs.uk/conditions/hearing-loss/)
- [Hearing loss - Wikipedia](https://en.wikipedia.org/wiki/Hearing_loss)
