# 3.10 Translating Identity Failure Into Operational Consequence

Identity findings gain significance when their technical effects are connected to the mission capabilities that depend on them.

This translation should be precise.

Not every excessive permission represents catastrophic mission risk. Not every credential exposure results in domain compromise. Not every certificate configuration grants useful authentication authority. Inflating every identity weakness into an existential threat makes technical reporting less credible and ultimately makes serious findings harder to distinguish.

The opposite mistake is equally damaging.

A directory permission that appears minor when viewed only at the object level may participate in a path whose final consequence is substantial. A service account that appears to support one application may authenticate across an entire server population. A synchronization platform categorized as middleware may possess administrative authority across two identity planes.

The practitioner has to follow the relationship far enough to establish actual consequence.
