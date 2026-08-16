# ERM-Format-Examples

This is the file format I use for rename maps to anybody who's interested.

```erm
erm {
  game="Demo"
}

asm name="Assembly-CSharp" {

# rename a specific type
typ name="OldType", namespace="Demo.Namespace" {
  name="NewType"
  namespace="Demo.Renamed"
}

# match using full type selectors
typ name="TargetType", namespace="Demo", base="UnityEngine.MonoBehaviour", flds=3, mtds=5, ifaces=1, nested=2, gargs=2, garg_names=["TKey","TValue"], acc=public, abstract=false, sealed=false, kind=class {
  name="FullyMatchedType"
}

# children is an alias for nested
typ children=2 {
  name="TypeWithTwoChildren"
}

# require a field and method to exist
typ {
  mem {
    fld name="health"
    mtd name="TakeDamage"
  }
  name="HasHealthAndDamage"
}

# require method and exclude another
typ {
  mem {
    mtd name="Update"
    !mtd name="FixedUpdate"
  }
  name="UpdateOnlyType"
}

# match field properties
typ {
  mem {
    fld name="speed", type="System.Single", acc=private, static=false
  }
  name="HasPrivateSpeedField"
}

# match field constant value
typ {
  mem {
    fld name="MaxPlayers", value=16
  }
  name="HasMaxPlayers"
}

# match different constant types
typ {
  mem {
    fld value=1800.0
    fld value=true
    fld value='A'
    fld value="Demo"
  }
  name="ConstantMatchedType"
}

# match method properties
typ {
  mem {
    mtd name="Move", type="System.Void", params=2, acc=public, static=false
  }
  name="MoveMethodType"
}

# match first parameter type
typ {
  mem {
    mtd name="Init" {
      prm[0] {
        typ name="System.String"
      }
    }
  }
  name="InitWithString"
}

# match parameter names
typ {
  mem {
    mtd name="Configure", param_names=["x","y","z"]
  }
  name="ConfigureXYZ"
}

# match generic type arguments
typ gargs=2, garg_names=["TKey","TValue"] {
  name="GenericType"
}

# match generic method arguments
typ {
  mem {
    mtd name="Convert", gargs=1, garg_names=["TResult"]
  }
  name="HasGenericConvert"
}

# match a generic argument
typ {
  mem {
    garg name="T"
  }
  name="HasGenericT"
}

# match a method generic argument
typ {
  mem {
    mtd name="Convert" {
      garg name="TResult"
    }
  }
  name="ConvertWithTResult"
}

# rename a generic argument
typ {
  garg[0] {
    name="TValue"
  }
}

# match a generic argument constraint
typ {
  mem {
    garg name="T" {
      typ name="System.Object"
    }
  }
  name="ConstrainedGenericType"
}

# match a specific generic argument constraint
typ {
  mem {
    garg name="T" {
      typ[0] name="System.Object"
    }
  }
  name="FirstConstraintObject"
}

# check first field name
typ {
  mem {
    fld[0] name="firstField"
  }
  name="FirstFieldMatch"
}

# check first method name
typ {
  mem {
    mtd[0] name="Awake"
  }
  name="FirstMethodAwake"
}

# check first generic argument
typ {
  mem {
    garg[0] name="T"
  }
  name="FirstGenericArgumentT"
}

# check field type
typ {
  mem {
    fld name="controller" {
      typ name="PlayerController"
    }
  }
  name="HasControllerField"
}

# check field type directly
typ {
  mem {
    fld name="controller", type="PlayerController"
  }
  name="HasControllerFieldDirect"
}

# check method return type
typ {
  mem {
    mtd name="GetPlayer" {
      typ name="Player"
    }
  }
  name="ReturnsPlayer"
}

# check method return type directly
typ {
  mem {
    mtd name="GetPlayer", type="Player"
  }
  name="ReturnsPlayerDirect"
}

# rename type of first field
typ {
  fld[0] {
    typ {
      name="Weapon"
      namespace="Game.Items"
    }
  }
}

# resolve nested type path
typ {
  mem {
    fld name="list" {
      typ[0] {
        name="ElementType"
      }
    }
  }
  name="ListHolder"
}

# match by base type
typ base="BaseClass" {
  name="DerivedRenamed"
}

# traverse base type
typ {
  mem {
    base typ name="BaseClass"
  }
  name="DerivedFromBaseClass"
}

# traverse an interface
typ {
  mem {
    iface typ name="IDamageable"
  }
  name="DamageableType"
}

# traverse a specific interface
typ {
  mem {
    iface typ[0] name="IDamageable"
  }
  name="FirstInterfaceDamageable"
}

# traverse nested types
typ {
  mem {
    nest typ name="NestedType"
  }
  name="HasNestedType"
}

# child is an alias for nest
typ {
  mem {
    child typ name="NestedType"
  }
  name="HasNestedChild"
}

# traverse a specific nested type
typ {
  mem {
    nest typ[0] name="NestedType"
  }
  name="FirstNestedType"
}

# traverse to declaring type
typ {
  mem {
    parent typ name="OuterType"
  }
  name="NestedInsideOuterType"
}

# traverse to adjacent type
typ {
  mem {
    adj typ[1] name="NextType"
  }
  name="BeforeNextType"
}

# traverse to previous type
typ {
  mem {
    adj typ[-1] name="PreviousType"
  }
  name="AfterPreviousType"
}

# match interfaces, structs, enums
typ kind=interface {
  name="RenamedInterface"
}

typ kind=struct {
  name="RenamedStruct"
}

typ kind=enum {
  name="RenamedEnum"
}

typ kind=class {
  name="RenamedClass"
}

# match access level
typ acc=private {
  name="PrivateTypeRenamed"
}

# match static field
typ {
  mem {
    fld name="Instance", static=true
  }
  name="SingletonType"
}

# match static method
typ {
  mem {
    mtd name="Create", static=true
  }
  name="HasStaticCreate"
}

# deep nested traversal
typ {
  mem {
    fld name="player" {
      typ {
        fld name="inventory" {
          typ {
            name="Inventory"
          }
        }
      }
    }
  }
  name="PlayerWithInventory"
}

# require one field and exclude another
typ {
  mem {
    fld name="enabled"
    !fld name="disabled"
  }
  name="EnabledOnly"
}

# require an exact stable member set
typ {
  mem checksum {
    fld name="health"
    fld name="speed"
    mtd name="Update"
  }
  name="ChecksummedType"
}

# combine nested requirements
typ {
  mem {
    mtd name="Create" {
      prm[0] {
        typ name="System.String"
      }

      garg[0] name="T"
    }

    iface typ name="System.IDisposable"
  }

  name="ComplexMatch"
}

# apply multiple child actions
typ {
  mem {
    mtd name="Start"
  }

  fld[0] {
    name="renamedField"
  }

  mtd[0] {
    name="RenamedMethod"
  }

  garg[0] {
    name="TRenamed"
  }

  name="MultiModifiedType"
}

# rename through base traversal
typ {
  base typ {
    name="RenamedBase"
  }
}

# rename through interface traversal
typ {
  iface typ[0] {
    name="RenamedInterface"
  }
}

# rename a nested type
typ {
  nest typ[0] {
    name="RenamedNestedType"
    namespace="Demo.Nested"
  }
}

# rename a parameter type
typ {
  mtd name="Init" {
    prm[0] {
      typ {
        name="RenamedParameterType"
      }
    }
  }
}

# rename a return type
typ {
  mtd name="GetValue" {
    typ {
      name="RenamedReturnType"
    }
  }
}

}
```
