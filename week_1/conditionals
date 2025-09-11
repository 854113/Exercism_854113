"""Functions to prevent a nuclear meltdown."""


def is_criticality_balanced(temperature, neutrons_emitted):
    """Verify criticality is balanced.

    :param temperature: int or float - temperature value in kelvin.
    :param neutrons_emitted: int or float - number of neutrons emitted per second.
    :return: bool - is criticality balanced?

    A reactor is said to be critical if it satisfies the following conditions:
    - The temperature is less than 800 K.
    - The number of neutrons emitted per second is greater than 500.
    - The product of temperature and neutrons emitted per second is less than 500000.
    """
    return (
        temperature < 800
        and neutrons_emitted > 500
        and (temperature * neutrons_emitted) < 500_000
    )


def reactor_efficiency(voltage, current, theoretical_max_power):
    """Assess reactor efficiency zone.

    :param voltage: int or float - voltage value.
    :param current: int or float - current value.
    :param theoretical_max_power: int or float - power that corresponds to a 100% efficiency.
    :return: str - one of ('green', 'orange', 'red', or 'black').

    Efficiency bands:
      - 'green'  : >= 80%
      - 'orange' : < 80% and >= 60%
      - 'red'    : < 60% and >= 30%
      - 'black'  : < 30%
    """
    generated_power = voltage * current
    efficiency_pct = (generated_power / theoretical_max_power) * 100

    if efficiency_pct >= 80:
        return 'green'
    if efficiency_pct >= 60:
        return 'orange'
    if efficiency_pct >= 30:
        return 'red'
    return 'black'


def fail_safe(temperature, neutrons_produced_per_second, threshold):
    """Assess and return status code for the reactor.

    :param temperature: int or float - value of the temperature in kelvin.
    :param neutrons_produced_per_second: int or float - neutron flux.
    :param threshold: int or float - threshold for category.
    :return: str - one of ('LOW', 'NORMAL', 'DANGER').

    Rules (p = temperature * neutrons):
      - 'LOW'    : p < 0.9 * threshold
      - 'NORMAL' : 0.9 * threshold <= p <= 1.1 * threshold
      - 'DANGER' : otherwise (i.e., p > 1.1 * threshold)
    """
