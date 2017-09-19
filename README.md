# opentron dna helix

from opentrons import containers, instruments

# a 12 row trough for sources
trough = containers.load('trough-12row', 'C2')

# plate to create dna helix in
plate = containers.load('96-PCR-flat', 'C1')

# a tip rack for our pipette
p200rack = containers.load('tiprack-200ul', 'A1')

# p200 (20 - 200 ul) single channel pipette
p200 = instruments.Pipette(
    axis="b",
    min_volume=20,
    max_volume=200,
    tip_racks=[p200rack],
)

# wells to dispense dinosaur body in green
red_wells = [ well.bottom() for well in plate.wells('B1', 'B2', 'C3', 'E5', 'F6', 'F7', 'E8', 'D9',
        'C10', 'B11', 'B12')]

# wells to dispense dinosaur back plates in blue
blue_wells = [well.bottom() for well in plate.wells('F1', 'F2', 'E3', 'D4', 'C5', 'B6', 'B7',
        'C8', 'E10', 'F11', 'F12')]

# red solution location
red = trough.wells('A1')
# blue solution location
blue = trough.wells('A2')

# macro commands like .distribute() make writing long sequences easier:
# distribute green solution to the body
p200.distribute(50, red, red_wells, disposal_vol=0, blow_out=True)
# distribute blue solution to the dinosaur's back
p200.distribute(50, blue, blue_wells, disposal_vol=0, blow_out=True)
