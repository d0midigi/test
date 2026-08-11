# 3.9 Identity Dependencies and Mission Assurance

Mission assurance requires understanding not only which systems perform mission functions but which systems allow those mission systems to establish trust.

The difference is easy to miss because identity dependencies are often quiet.

A database may run for months without anyone discussing Active Directory.

A command application may authenticate automatically through existing sessions.

A certificate may remain valid for years.

A service account may execute continuously without a human entering its password.

The identity dependency becomes visible only when something changes.

A Domain Controller becomes unavailable.

A certificate expires.

A trust breaks.

A service-account password is rotated incorrectly.

A user is removed from a group.

A federation signing key changes.

A synchronization process fails.

The application that appeared independent suddenly stops functioning.

Mission assurance therefore requires visibility into identity dependencies before they become outages.
