### Importing Data files

On web bash;

1. Run `python manage.py migrate`


2. Load mapit country, types and code types from a fixture

```
python manage.py loaddata geo/fixture.json
```

3. Create new `generation` to import data into

```
python manage.py mapit_generation_create \
   --desc='Adding boundaries' --commit
```
For a fresh project, generation with id 1 will be created


4. Then import geojson files as follows. Nigeria as example

- importing country

```
python manage.py mapit_import --commit \
        --generation_id=1 --country_code=NG --area_type_code=COUNTRY \
        --name_type_code=Binfo --name_field=name \
        --code_type=AFR --code_field=afr_geoid \
        geo/Nigeria/country.geojson
```

- importing state

```
python manage.py mapit_import --commit \
        --generation_id=1 --country_code=NG --area_type_code=STATE \
        --name_type_code=Binfo --name_field=name \
        --code_type=AFR --code_field=afr_geoid \
        geo/Nigeria/state.geojson
```

- importing local government areas

```
python manage.py mapit_import --commit \
        --generation_id=1 --country_code=NG --area_type_code=LOCAL-GVT \
        --name_type_code=Binfo --name_field=name \
        --code_type=AFR --code_field=afr_geoid \
        geo/Nigeria/local_government.geojson
```

5. Once you finish importing all countries geojsons file, you can now activate generation with the following command:

```
 python manage.py mapit_generation_activate --commit

```

To map area with parent, run the following command which uses the `geos_parent_map.csv` to load parent areas

```
 python manage.py mapit_load_parent_area
```

For country based application, we import country based codes. To do so you can run

```
 python manage.py mapit_add_country_codetype
```