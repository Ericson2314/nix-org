# Constitution Commentary

This document contains a non-normative, non-binding commentary on the constitution, explaining some subtleties.

## SC Election, Removal, and Dissolution procedure

The state machine of these portions of the constitution is especially complex.

These interactions are of special note:

- When less than half of the seats are filled, if any SC member proposes a no confidence vote, the vote will automatically win due to how vacant seats are counted for dissolution votes.
  However if the SC does not hold such vote, and is thus unanimous in choosing to hold a special election for the currently-vacant seats only instead, such a special election will proceed.

- It is only possible to follow a dissolution with an initial election when more than half of the SC seats were full prior to dissolution.

- Vacant seats not triggering a dissolution vote makes it possible for the vacancy procedure for when less than half of the seats are filled to resolve the situation without dissolution.

- After a removal has occurred, it is possible to hold a special election to fill the vacant seat.

The following flow chart diagrams the procedure, hopfully making these interactions explicit:

```mermaid
flowchart TD
    Start([Regular SC Governance])
    Start -.->|optional| Removal
    Start -.->|optional| Dissolution
    Start -.->|optional, if <7 filled| SpecialElec
    %% Removal for Conduct
    Removal[Vote for conduct] -->|succeeds by supermajority| OneMoreVacation[[one additional seat vacant]] --> VacancyCheck
    Removal -->|fails| Start
    %% Dissolution
    Dissolution[Vote to dissolve the SC<br/>vacant seats vote yes] -->|succeeds by majority| AllVacated0[[all seats vacated]] --> ElectionType[Vote between election types<br/>vacant seats vote special]
    Dissolution -->|fails| Start
    ElectionType -->|initial wins| InitialElec
    ElectionType -->|special wins| SpecialElec
    %% Vacancy Check
    VacancyCheck{Vacancy count?}
    VacancyCheck -->|≥4 filled| Start
    VacancyCheck -->|<4 filled| Required[Vote for Special Election or dissolution]
    Required -.->|all members propose special election| SpecialElec
    Required -.->|any member proposition dissolution| X[[all seats vacated]] -->|special election wins via vacant seat votes| SpecialElec
    %% Special Elections
    SpecialElec[Special Election] -->|winners serve remainder of terms| Start
    %% Initial Elections
    InitialElec[Initial Election] -->|Entirely new SC seated</br>top 4: 2yr terms<br/>bottom 3: 1yr terms| Start
```
