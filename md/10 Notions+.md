# 10. Notions+

1. strain rate는 thermal diffusivity(alpha)/unstretched laminar flame speed(Sl0)로 정의하고, 여기서 사용하기 위해 thermal diffusivity와 unstretched laminar flame speed를 계산
2. thermal diffusivity는 화염의 초기 상태에서 계산됨. 그리고 초기 연료 혼합물의 thermal conductivity(lambda), density, cp가 고정된 값이므로 열 확산 계수도 고정됨. 따라서 특정 조건(초기 상태)에서 한 번만 계산하면 됨.
3. thermal diffusivity는 화염 전반에 영향을 미치는 전역 특성으로, 공간적으로 변하지 않는다고 가정. 예를 들어, 계산된 열 확장 계수는 화염의 strain rate(strain에 따른 변형 속도)를 계산하는 데 사용됨. 이는 화염의 전체 거동에 중요한 값이므로, 위치별로 계산할 필요가 없음.
4. `Xflame`은 코드 안에서 **화염의 최종 상태에서의 화학 조성**을 나타냄. 화염의 각 위치에서 모든 화학 종의 조성을 나타내는 2D 배열의 마지막 열을 선택하여 [:, -1] **화염의 최종 위치에서의 화학 조성**을 추출.
5. `Xflame`을 사용하여 연료의 최종 농도를 확인하고, 연소로 인해 소모된 연료의 양을 계산함. 소모량은 **ScF** 계산에 직접적으로 사용. 아래 코드 참고
6. **`Xflame`**은 **몰 분율**을 저장하고 있고, ScF 계산에서는 **질량 분율**이 필요해서 ****`flame.Y` 사용. **`mass_fraction_diff`** 에 사용된 형태가 같은 화염 최종 상태의 데이터를 다른 단위(질량 분율 대신 몰 분율)로 저장한 것.

```python
mass_fraction_diff = sum(flame.Y[gas.species_index(fuel), -1] - flame.Y[gas.species_index(fuel), 0] for fuel in fuel_species)
```

---

# ⚡️ todos

1. Set the **project temperature** by tweaking the adiabatic temp using **Ka** and **beta** to keep things stable and consistent.
2. Compare results with Garcia2022a graphs to spot similarities or differences.