---
permalink: /teaching/
title: "Teaching"
---


I have been the TA for a 4th year mechanical engineering module for the past 4 years (<a href="https://www.tcd.ie/Engineering/assets/module-descriptors/ss/MEU44B17.pdf" target="_blank">MEU44B17</a>). The subject matter relates to the the kinematics and dynamics of multibody systems (systems of rigid bodies connected by kinematic joints). It reviews fundamental linear algebra methods, and introduces students to the 3D rotation group or the special orthogonal group in three dimensions (SO(3)) for three-dimensional kinematics and dynamics operations. The module aims to equip students with theoretical and practical knowledge for computational modelling of multibody systems. Applications include human body modeling for gait and impact analysis, and robotics.

**Videos:**

{% include video id="JHGY1VYZuTw" provider="youtube" %}


{% include video id="OSsWPNQaOHI" provider="youtube" %}


{% include video id="k97Rn_Bl82s" provider="youtube" %}


**Blog posts:**

> | <a href="https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/#the-3d-rotation-group" target="_blank">The 3D rotation group</a> |
> | <a href="https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/#mapping-of-two-vectors" target="_blank">Non-uniqueness of the Euler axis in vector mapping</a> |
> | <a href="https://kevgildea.github.io/blog/Kinematic-Chain-Mapping/#definining-a-kinematic-chain-and-applying-forward-kinematics" target="_blank">Definining a kinematic chain and applying forward kinematics</a> |
> | <a href="https://kevgildea.github.io/blog/Kinematic-Chain-Mapping/#solution-space-for-mapping-kinematic-chains" target="_blank">Solution space for mapping serial kinematic chains: A modified inverse/forward kinematics approach</a> |
> | <a href="https://kevgildea.github.io/blog/Kinematic-differential-equations/" target="_blank">Euler integration of kinematic differential equations for position and orientation</a> |
> | <a href="https://kevgildea.github.io/blog/EOM-contact-modelling/" target="_blank">Computational modelling of a bouncing ball using differential equations of motion</a> |

\begin{align*}
\resizebox{1\textwidth}{!}{
\begin{matrix}
\mathrm{\left[ \mathrm{R}^{\widehat{a}\to \widehat{b}}\right]}^{EAS} =  \\
\left[ \begin{matrix}
{n}_{\alpha,1}^{2} + ({n}_{\alpha,2}^{2}+ {n}_{\alpha,3}^{2})cos({\Phi}_{\alpha}) & {n}_{\alpha,1}{n}_{\alpha,2}(1-cos({\Phi}_{\alpha}))-{n}_{\alpha,3}sin({\Phi}_{\alpha}) & {n}_{\alpha,1}{n}_{\alpha,3}(1-cos({\Phi}_{\alpha}))+{n}_{\alpha,2}sin({\Phi}_{\alpha})\\
{n}_{\alpha,1}{n}_{\alpha,2}(1-cos({\Phi}_{\alpha}))+{n}_{\alpha,3}sin({\Phi}_{\alpha}) & {n}_{\alpha,2}^{2} + ({n}_{\alpha,1}^{2}+ {n}_{\alpha,3}^{2})cos({\Phi}_{\alpha}) & {n}_{\alpha,2}{n}_{\alpha,3}(1-cos({\Phi}_{\alpha}))-{n}_{\alpha,1}sin({\Phi}_{\alpha})\\
{n}_{\alpha,1}{n}_{\alpha,3}(1-cos({\Phi}_{\alpha}))-{n}_{\alpha,2}sin({\Phi}_{\alpha}) & {n}_{\alpha,2}{n}_{\alpha,3}(1-cos({\Phi}_{\alpha}))+{n}_{\alpha,1}sin({\Phi}_{\alpha}) & {n}_{\alpha,3}^{2} + ({n}_{\alpha,1}^{2}+ {n}_{\alpha,2}^{2})cos({\Phi}_{\alpha})
\end{matrix} \right]
\end{matrix}
}
\end{align*}
