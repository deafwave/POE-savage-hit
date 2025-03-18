# POE-savage-hit

Savage hit calculations for Path of Exile [Vengeful Cry](https://www.poewiki.net/wiki/Vengeful_Cry)

## [SageMathCell](https://sagecell.sagemath.org/)

```
var('l,e,c')

# Character Stats
max_life = 4786
max_es = 7217
chaos_res = 71
progenesis = True
petrifiedblood = False
fortify = 20

# Cleanliness
progenesis_modifier = 0.25 if progenesis else 0
petrifiedblood_modifier = 0.6 if petrifiedblood else 0
fortify_modifier = 1 - (0.01 * fortify)

forbidden_rite_damage = (l*0.4 + e*0.25) * (1 - c) * (1 - petrifiedblood_modifier - progenesis_modifier) * fortify_modifier
savage_hit_threshold = l * 0.15

# Evaluate if damage is above threshold at given values
l_value = max_life / 10000
e_value = max_es / 10000
c_value = chaos_res / 100
damage_at_point = forbidden_rite_damage.subs({l: max_life/10000, e: max_es/10000, c: chaos_res/100})
threshold_at_point = savage_hit_threshold.subs({l: max_life/10000})
sphere_color = "cyan" if damage_at_point > threshold_at_point else "red"

# Plot
S = implicit_plot3d(forbidden_rite_damage == savage_hit_threshold, (l, 0, 2), (e, 0, 5), (c, 0, 0.81),
                    axes_labels=['Life', 'Energy Shield', 'Chaos Res']
                   )
S += sphere((l_value, e_value, c_value), size=0.05, color=sphere_color)
S.show()
```
![Savage Hit Acquired](https://github.com/user-attachments/assets/ffab78de-ff51-4865-bf2d-766b7cdfe551)
