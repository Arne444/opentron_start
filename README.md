# opentron dna helix

### dna helix pattern - 96-well plate

# change well_volume to set final volume of all wells in the 96-well plate
well_volume = 200

# a 12 row trough for sources
trough = containers.load('trough-12row', 'C2')

# plate to create dna helix in
plate = containers.load('96-PCR-flat', 'C1')

# a tip rack for pipette
p200rack = containers.load('tiprack-200ul', 'A1')

# p200 (20 - 200 ul) single channel pipette
p200 = instruments.Pipette(
    axis="b",
    min_volume=20,
    max_volume=200,
    tip_racks=[p200rack],
    trash_container=trash)

# distribute 100 ul H20 to wells
blue_h2o_wells = [ well.bottom() for well in plate.wells (‘B1', ‘B2', ‘C3’, 'D4’, 'E5’, 'F6’, ‘F7’, 'H3', ‘E8’, ‘C10’, ‘B11’, ‘B12’)]

# distribute 100 ul H2O to wells
red_h2o_wells =  [ well.bottom() for well in plate.wells (’F1’, ‘F2’, ‘E3’, ‘C5’, ‘B6’, ‘B7', ‘C8’, ‘D9’, ‘E10’, ‘F11’, ‘F12’)]

# wells to dispense blue strand
blue_wells = [ well.bottom() for well in plate.wells (‘B1’)

# wells to dispense red strand
red_wells = [well.bottom() for well in plate.wells(‘F12’)

# H2O solution location
dna = trough.wells('A1')
# blue solution location
blue = trough.wells('A2')
# red solution location
Red = trough.wells(‘A3’)

# distribute H2O to all wells
p200.distribute(100, dna, blue_h2o_wells, disposal_vol=0, blow_out=True)
P200.distribute(100, dna, red_h2o_wells, disposal_vol=0, blow_out=True)
P200.distribute(300, blue, blue_wells, disposal_vol=0, blow_out=True)
P200.distribute(300, red, red_wells, disposal_vol=0, blow_out=True)

#Transfer 100 ul blue solution between wells
m200.transfer(
	100, 
	blue_h2o_wells(‘1’, to=’12’),
	red_h2o_wells(‘1’, to=’12’)
)
              
