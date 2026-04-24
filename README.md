# ERM-Format-Examples

This is the file format I use for rename maps to anybody who's interested.

``` erm
erm {
  game="TestGame",
  build="1.0.0"
} erm

asm name="Assembly-CSharp" {

    # full selector with all actions applied
    typ name="Controller",namespace="Core.Systems",flds=4,mtds=10,ifaces=1,gargs=0,acc=public,abstract=false,sealed=false,kind=class {
        name="ControllerRenamed"
        namespace="Core.Systems.Renamed"

        base_type_name="BaseController"
        base_type_namespace="Core.Framework"

        mem {
            mtd name="Update",ret="System.Void",params=1,param_names=["dt"],gargs=0,acc=public,static=false {
                type_name="UpdateResult"
                type_namespace="Core.Results"

                param_type_name[0]="System.Single"
                param_type_namespace[0]="System"
            } mtd

            !mtd name="DebugLog"

            fld name="state",type="System.Int32",acc=private,static=false {
                type_name="StateValue"
                type_namespace="Core.Types"
            } fld

            !fld name="temp"
        } mem

        mtd name="Reset" { name="ResetState" } mtd
        mtd params=0 { name="NoParamMethod" } mtd
        mtd gargs=1 { name="GenericMethodRenamed" } mtd
        mtd acc=protected { name="ProtectedMethod" } mtd
        mtd static=true { name="StaticMethod" } mtd
        mtd param_names=["value"] { name="SetValue" } mtd

        fld name="state" { name="currentState" } fld
        fld type="System.Int32" { name="intStorage" } fld
        fld acc=private { name="privateField" } fld
        fld static=true { name="staticField" } fld
    } typ


    # identifies type using a field and renames that field's type
    typ {
        mem {
            fld name="target" {
                type_name="TargetObject"
                type_namespace="Core.Objects"
            } fld
        } mem

        name="TargetHandler"
    } typ


    # identifies type using method return type and renames it
    typ {
        mem {
            mtd name="Create",ret="System.Object" {
                type_name="FactoryProduct"
                type_namespace="Core.Factory"
            } mtd
        } mem

        name="FactoryWrapper"
    } typ


    # identifies type using parameter type and renames it
    typ {
        mem {
            mtd name="Initialize",params=1 {
                param_type_name[0]="InitContext"
                param_type_namespace[0]="Core.Init"
            } mtd
        } mem

        name="Initializer"
    } typ


    # selector-less inference using only an action
    typ {
        mem {
            fld {
                type_name="SharedData"
                type_namespace="Core.Shared"
            } fld
        } mem

        name="SharedContainer"
    } typ


    # excludes types that contain a specific method
    typ {
        mem {
            !mtd name="Dispose"
            fld name="data"
        } mem

        name="PersistentData"
    } typ


    # matches using only anchors
    typ {
        mem {
            mtd name="Tick"
            fld name="instance"
        } mem

        name="TickSystem"
    } typ


    # renames base type through a known derived type
    typ name="DerivedComponent" {
        base_type_name="ComponentBase"
        base_type_namespace="Core.Components"
    } typ


    # enum match
    typ name="StatusCode",kind=enum,acc=public {
        name="StatusCodeRenamed"
    } typ


    # struct match
    typ name="Point2D",kind=struct,sealed=true {
        name="Vec2"
    } typ


    # interface match
    typ name="IRenderable",kind=interface,abstract=true {
        name="IRenderableRenamed"
    } typ


    # matches empty internal type
    typ acc=internal,flds=0,mtds=0 {
        name="EmptyInternal"
    } typ


    # matches using parameter names only
    typ {
        mem {
            mtd param_names=["entity","index"]
        } mem

        name="ParamMatch"
    } typ
}
asm
```
