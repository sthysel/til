# Notes on django import-export

## Resource
    * import_data(dataset)
        * RESULT
        * before_import(dataset) <H>
        * for each row in dataset:
            * get_or_init_instance(row)
                * get || init
            * for_delete(instance)
            * import_obj(instance, row)
                * for each field in Resource:
                * import_field(field, instance, data)
                    * if (field.attribute && field.column_name)
                        * field.save(instance)
                            attribute = field.clean(data)
            * skip_row(updated_object, original_object)
            * before_save_instance(instance) <H>
            * save_instance(instance) <H>
            * after_save_instance(instance) <H>
            * save_m2m()
            * Add row result to RESULT


## hydrate

For some reason dehydrate is also called on import, why ?

```
def dehydrate_lat(self, resource):
    if resource.site:
        return resource.site.get_lat()
```
