# ncids-with-uswds-patch-sync
Test of patching and syncing USWDS for NCIDS

## Notes about this setup
1. USWDS should be installed as a dev dependency since we don't want dependent projects to download it. 
1. this uses yarn to be more like NCIDS-css
   1. The patching process is different for yarn than npm, so this will mimick our setup best.
1. 

## Notes about USWDS
* `packages/uswds-tokens/color/*` - this appears to be json related to documentation or something. Maybe not needed? Only referenced in `format-tokens` npm script.
  * This could probably be removed -- will ignore for now updating colors.

### Changes
<table>
  <tr><td colspan="3">System Token Changes</td></tr>
  <tr><td colspan="3">Colors</td></tr>
  <tr>
    <th>Step</th>
    <th>Changed from USWDS</th>
    <th>What to do</th>
  </tr>
  <tr>
    <td>1.</td>
    <td>
      We added color token partials (in `ncids-css/scss/core/ncids-system-tokens`) to the system tokens and changed the imports in the system tokens file to add:
      * _cerulean.scss
      * _cranberry.scss
      * _golden.scss
      * _navy.scss
      * _teal.scss
    </td>
    <td>
      Add the partials to `uswds-core/src/styles/tokens/color`
    </td>
  </tr>
  <tr>
    <td>2.</td>
    <td>
      We updated $system-colors to add the new color partials to the colors.
    </td>
    <td>
      Update `uswds-core/src/styles/tokens/color/system-colors.scss` to add the new colors.
    </td>
  </tr>
  <tr>
    <td>3.</td>
    <td>
      We updated $tokens-color-basic to add
      * "cranberry": get-system-color("cranberry", 50),
      * "cerulean": get-system-color("cerulean", 50),
      * "navy": get-system-color("navy", 50),
      * "golden": get-system-color("golden", 50),
      * "teal": get-system-color("teal", 50),
    </td>
    <td>
      1. Update `uswds-core/styles/tokens/color/shortcodes-color-basic.scss` to add our colors.
    </td>
  </tr>
  <tr>
    <td>4.</td>
    <td>
      * Added `$color-<color>-<level>`:
        * For colors:
          * cranberry
          * Cerulean
          * Navy
          * Golden
          * Teal
        * For levels 5-90, 5v-90v
      * Added all the `$color-<color>-<level>` colors to the $system-color-shortcodes
    </td>
    <td>
      Update `uswds-core/src/styles/tokens/color/shortcodes-color-system.scss` to:
      * add the `$color-<color>-<level>` variables
      * add those items to `$system-color-shortcodes`
    </td>
  </tr>
  <tr><td colspan="3">Fonts</td></tr>
  <tr>
    <th>Step</th>
    <th>Changed from USWDS</th>
    <th>What to do</th>
  </tr>
  <tr>
    <td>1.</td>
    <td>
        1. Added `poppins` to the `$system-typeface-tokens`
        2. Removed the src element for roboto-mono.
           * This is so we can use Google Fonts
        
        NOTE: we also removed some other stuff.
    </td>
    <td>
        Edit `uswds-core/src/styles/tokens/font/typefaces.scss` to:
        * Add Poppins
        * remove the src element from all fonts
          * we should only be recommending Google Fonts
            * We should not be recommending these font's anyway...
    </td>
  </tr>
  <tr><td colspan="3">Settings</td></tr>
  <tr>
    <th colspan="2">Changed from USWDS</th>
    <th>What to do</th>
  </tr>
  <tr>
    <td colspan="2">
      Changed in `_settings-typography.scss`
      * Added imports for Google web fonts
      * Changed `$theme-font-type-sans` to `open-sans`
      * Changed `$theme-font-type-serif` to `poppins`
      * Changed the following `$theme-type-scale-XXX` sizes
        * xs --> 5
        * sm --> 7
        * md --> 8
        * xl --> 10
        * 2xl --> 11
        * 3xl --> 12
      * Changed `$theme-font-weight-bold` to 600
      * Changed `$theme-body-font-size` to xs
        * our xs is the same size as sm, (~16px) and our sm is larger
    </td>
    <td>
      Update `uswds-core/src/styles/settings/_typography.scss`
      * Changed `$theme-font-type-sans` to `open-sans`
      * Changed `$theme-font-type-serif` to `poppins`
      * Changed the following `$theme-type-scale-XXX` sizes
        * xs --> 5
        * sm --> 7
        * md --> 8
        * xl --> 10
        * 2xl --> 11
        * 3xl --> 12
      * Changed `$theme-font-weight-bold` to 600
      * Changed `$theme-body-font-size` to xs

      >**_NOTE:_** I did not move in the Google fonts. They should be managed elsewhere in all of this if someone uses the theme overrides to change the font.
    </td>
  </tr>
  <tr>
    <td colspan="2">
      Changed `_settings-color.scss`
      * Changed `$theme-color-primary-*` colors from blue to cerulean.
      * Changed `$theme-color-secondary-*` colors from red to teal.
      * Changed `$theme-color-accent-warm-*` from orange to golden. 
      * Changed `$theme-color-accent-cool-*` from blue cool to navy
      * Changed `$theme-color-error-*` colors from red-warm to cranberry
      * Changed `$theme-color-warning-*` colors from gold to golden
      * Changed `$theme-color-success-*` colors from green-cool to teal
      * Changed `$theme-color-info-*` colors from cyan to cerulean
      * Changed `$theme-color-emergency` and `$theme-color-emergency-dark` to cranberry
      >**_NOTE:_** Almost all of the colors had weighting changes. In some cases the original USWDS fonts used vivid or even other colors. (e.g. blue-warm) (The USWDS seems to have a wider gamut)
    </td>
    <td>
      Update `uswds-core/src/styles/settings/_typography.scss` to make the same changes.
    </td>
  </tr>
  <tr>
    <td colspan="2">Changed `_settings-general.scss` to turn off notifications</td>
    <td>Left it on -- we should turn it off when we use it, but others might want it</td>
  </tr>
  <tr>
    <td colspan="2">Changed `_settings-spacing.scss to set the `$theme-grid-container-max-width` to `widescreen`.</td>
    <td>Update `uswds-core/src/styles/settings/_settings-spacing.scss`</td>
  </tr>
  <tr>
    <td colspan="2">Changed `_settings-utilities.scss` to enable widescreen utility generation.</td>
    <td>Update `uswds-core/src/styles/settings/_settings-utilities.scss` to do the same.</td>
  </tr>
  <tr>
    <td colspan="2">
        Changed `_settings-components.scss` for:
        * Set `$theme-banner-max-width` to be widescreen
        * Set `$theme-breadcrumb-font-size` to 2xs
        * Set `$theme-footer-max-width` to widescreen
        * Set `$theme-header-max-width` to widescreen
        * Set `$theme-identifier-max-width` to widescreen 
        * Set `$theme-navigation-font-family` to heading
        * Set `$theme-site-alert-max-width` to widescreen
    </td>
    <td></td>
  </tr>

</table>




System Token Changes
* Fonts
    1. Removed $system-font-stack-georgia
    2. Removed $system-font-stacks ???
        * This might have been something added that we missed on an upgrade.
    3. Changes to $system-typeface-tokens:
        * Removed System
        * Removed Georgia
        * Removed Tahoma
        * Removed Verdana
        * Removed merriweather
        * Added Poppins
        * Removed src for robot-mono
        * Removed source-sans-pro
        * Removed public sans
* Colors
    1. We changed the imports for colors to be uswds instead of ./. The colors are:
        * Red-cool
        * Red
        * Red-warm
        * Orange-warm
        * Orange
        * Gold
        * Yellow
        * Green-warm
        * Green
        * Green-cool
        * Mint
        * Mint-cool
        * Cyan
        * Blue-cool
        * Blue
        * Blue-warm
        * Indigo-cool
        * Indigo
        * Indigo-warm
        * Violet
        * Violet-warm
        * Gray-cool
        * Gray
        * Gray-warm
    2. We added the following local uswds imports
        * Cranberry
        * Cerulean
        * Navy
        * Golden
        * Teal
    3. We updated $system-colors to add
        * Cranberry
        * Cerulean
        * Navy
        * Golden
        * Teal
    4. We updated $tokens-color-basic to add
        * "cranberry": get-system-color("cranberry", 50),
        * "cerulean": get-system-color("cerulean", 50),
        * "navy": get-system-color("navy", 50),
        * "golden": get-system-color("golden", 50),
        * "teal": get-system-color("teal", 50),
    5. Added $color-<color>-<level>:
        * For colors:
            * cranberry
            * Cerulean
            * Navy
            * Golden
            * Teal
        * For levels 5-90, 5v-90v
    6. Added all the $color-<color>-<level> colors to the $system-color-shortcodes
    7. Removed the $high-contrast-system-colors
        * This is probably another mistake when updating where it was added and then no one copied it over.

Package Changes
* Global
    * We removed normalize
    * We added accessibility
* Required
    * Replaced all settings with ours
    * Uses local system tokens
    * Uses USWDS:
        * Functions
        * Variables
        * Mixins (all)
        * Placeholders (all)
* Utilities
    * Changed name from uswds-utilities
    * Added no-print utility

